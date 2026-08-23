# Classification: From a Question to a Valid Prediction

Classification is a **supervised machine-learning task** in which the target is a category or class.

Examples:

* Will a customer **buy / not buy**?
* Is an email **spam / not spam**?
* Which species does an observation belong to?
* Will a task be **submitted on time / late**?

The important point is that the class we want to predict is already known for the examples used to train the model.

Classification therefore starts with a question:

> **What categorical outcome are we trying to predict, and what information would actually be available when the prediction is made?**

---

## 1. Observations, features and target

A classification dataset normally contains:

* **observations** – the cases being studied;
* **features** – information used to make predictions;
* **target** – the class to be predicted.

In scikit-learn these are commonly written as:

* `X` = features
* `y` = target

For example:

| study_hours | previous_score | attempts | outcome |
| ----------: | -------------: | -------: | ------- |
|          12 |             72 |        1 | pass    |
|           5 |             41 |        3 | fail    |
|           9 |             65 |        2 | pass    |

Here:

* one row represents one observation;
* `study_hours`, `previous_score` and `attempts` are possible features;
* `outcome` is the target.

The target must have a meaningful relationship to the problem. A column should not become a target merely because it happens to exist in the dataset.

---

## 2. Binary and multiclass classification

A **binary classification** problem has two classes.

Examples:

* yes / no
* pass / fail
* fraud / not fraud

A **multiclass classification** problem has more than two possible classes.

Examples:

* low / medium / high
* cat / dog / horse
* product category A / B / C / D

Many classification methods can handle both binary and multiclass problems. For example, scikit-learn's logistic regression and decision-tree classifiers support multiclass classification. ([Scikit-learn][1])

Classification is different from:

* **regression**, where the target is numerical;
* **clustering**, where predefined target labels are not available;
* **association analysis**, where the goal is to find patterns of co-occurrence.

---

## 3. Training and testing

A model should not be evaluated using the same observations that were used to fit it.

The usual first step is therefore to divide the available labelled data into:

**training data**
→ used to fit the model

**test data**
→ kept separate and used to evaluate predictions on unseen observations

Scikit-learn provides `train_test_split()` for this purpose. ([Scikit-learn][2])

A basic workflow is:

**prepare problem → define X and y → split → fit → predict → evaluate**

For example:

```python
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression

X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.25,
    random_state=42,
    stratify=y
)

model = LogisticRegression(max_iter=1000)

model.fit(X_train, y_train)

y_pred = model.predict(X_test)
```

`stratify=y` can be useful when we want approximately the same class proportions in the training and test sets.

The general `fit()` → `predict()` workflow is shared by scikit-learn classifiers, which makes it relatively easy to compare different methods. The ISLP classification lab demonstrates the same workflow with logistic regression, LDA, QDA, Naive Bayes and KNN. ([intro-stat-learning.github.io][3])

---

## 4. Prediction is not the same as probability

A classifier can return a predicted class:

```python
model.predict(X_test)
```

Many classifiers can also return estimated probabilities for the possible classes:

```python
model.predict_proba(X_test)
```

For example, a binary model might produce:

| P(fail) | P(pass) | prediction |
| ------: | ------: | ---------- |
|    0.08 |    0.92 | pass       |
|    0.61 |    0.39 | fail       |

Logistic regression explicitly models class probabilities and can convert those probabilities into class predictions. ([Scikit-learn][4])

A probability estimate is not certainty. A model predicting a probability of `0.70` is not saying that the event is guaranteed to occur.

---

## 5. Start with a baseline

A complicated classifier is useful only if it performs better than a simple alternative.

Imagine that 90% of observations belong to class A.

A model that always predicts A already has:

**90% accuracy**

without using any features at all.

This is why a useful classification exercise should include a **baseline**.

Scikit-learn provides `DummyClassifier`, which deliberately ignores the feature values and makes simple predictions such as always choosing the most frequent class. It exists specifically as a baseline for comparison with real classifiers. ([Scikit-learn][5])

Ask:

> **Does the model actually learn something useful compared with a trivial prediction?**

---

## 6. Accuracy is useful, but not sufficient

Accuracy is the proportion of predictions that are correct. ([Scikit-learn][6])

For example:

100 observations
90 correct predictions

gives:

**accuracy = 0.90**

But accuracy can hide important mistakes.

Suppose only 5 of 100 observations belong to the important positive class. A model that predicts the negative class for everybody has:

**95% accuracy**

but detects none of the positive cases.

Therefore, we need to inspect the types of errors.

---

## 7. Confusion matrix

A confusion matrix compares the actual classes with the predicted classes.

For binary classification:

|                     | Predicted negative | Predicted positive |
| ------------------- | -----------------: | -----------------: |
| **Actual negative** |      True Negative |     False Positive |
| **Actual positive** |     False Negative |      True Positive |

Scikit-learn defines confusion-matrix entry (C_{i,j}) as the number of observations whose actual class is (i) and predicted class is (j). ([Scikit-learn][7])

In Python:

```python
from sklearn.metrics import confusion_matrix

confusion_matrix(y_test, y_pred)
```

The confusion matrix helps answer a more useful question than simply:

> How many predictions were correct?

It shows:

> **What kinds of mistakes did the classifier make?**

---

## 8. Precision and recall

Two important measures can be derived from the confusion matrix.

### Precision

Precision asks:

> **Of the cases predicted as positive, how many really were positive?**

[
Precision =
\frac{TP}{TP + FP}
]

High precision means relatively few false positive predictions.

### Recall

Recall asks:

> **Of all actual positive cases, how many did the classifier find?**

[
Recall =
\frac{TP}{TP + FN}
]

High recall means relatively few positive cases were missed. ([Scikit-learn][6])

Which one matters more depends on the problem.

For example:

* medical screening may place strong importance on avoiding missed cases;
* automatic blocking systems may place strong importance on avoiding incorrect accusations.

There is no universally best evaluation metric. The metric should reflect the actual consequences of classification errors.

The **F1 score** combines precision and recall and can be useful when both matter, but you should still understand the underlying false positives and false negatives. ([Scikit-learn][6])

---

## 9. Preprocessing can cause data leakage

This is one of the most important rules in the classification workflow.

Suppose we scale a numerical feature using its mean and standard deviation.

If we calculate those values from the **whole dataset before splitting**, the test data has already influenced the preprocessing.

Information has leaked from the test set into model development.

The same problem can occur with:

* scaling;
* missing-value imputation;
* feature selection;
* dimensionality reduction;
* many other transformations.

Scikit-learn recommends splitting training and test data **before fitting preprocessing operations**. Transformations should learn their parameters from the training data and then apply the same transformation to the test data. Pipelines help enforce this workflow. ([Scikit-learn][8])

Correct principle:

**split first → fit preprocessing on training data → transform training and test data → fit model**

A pipeline can combine preprocessing and modelling:

```python
from sklearn.pipeline import make_pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression

model = make_pipeline(
    StandardScaler(),
    LogisticRegression(max_iter=1000)
)

model.fit(X_train, y_train)
y_pred = model.predict(X_test)
```

Pipelines reduce the risk of accidentally applying preprocessing inconsistently or leaking test information into training. ([Scikit-learn][8])

---

## 10. A few classifiers are enough to understand the workflow

This week is not about memorizing a long list of algorithms.

The important goal is to understand the **classification process**.

Three useful examples are:

### Logistic regression

Despite its name, logistic regression is commonly used as a classifier. It estimates class probabilities and provides a relatively simple baseline model. ([Scikit-learn][4])

### Decision tree

A decision tree classifies observations by repeatedly splitting the feature space according to feature values.

Trees are useful because the sequence of decisions can often be inspected and explained. ([Scikit-learn][9])

### K-nearest neighbours

KNN predicts a class based on nearby observations.

It provides a useful demonstration of why the scale of numerical features can matter: a variable measured on a large numerical scale may dominate distance calculations unless the data is prepared appropriately. The ISLP classification lab includes both scaling and KNN examples. ([intro-stat-learning.github.io][3])

Naive Bayes is another useful simple baseline, particularly for some high-dimensional problems. ([Pythonic Perambulations][10])

You do **not** need to master all of these algorithms before Monday.

You should understand how a classifier fits into the overall workflow.

---

## 11. Model comparison must be fair

Suppose model A obtains 82% accuracy and model B obtains 85%.

It is tempting to declare model B better.

Before doing that, ask:

* Were both evaluated on the same test observations?
* Was preprocessing performed correctly?
* Is accuracy the appropriate metric?
* Is the difference large enough to matter?
* How many observations were available?
* Are some classes rare?
* Was the test set repeatedly used while developing the models?

The test set should represent **unseen data**, not become another training resource.

Later in the course we will study validation and model comparison in more depth. Zaki & Meira devote a separate chapter to classification performance measures and classifier evaluation. ([Data Mining and Machine Learning][11])

---

## 12. Classification must fit the problem

Before building a classifier, ask:

1. **Is the target genuinely categorical?**
2. **What does one observation represent?**
3. **Which variables would actually be available when the prediction is made?**
4. **Could any feature reveal the target indirectly?**
5. **Do we have enough examples of the different classes?**
6. **What would false positives and false negatives mean?**
7. **Would making this prediction actually be useful and appropriate?**

A technically possible prediction is not automatically a meaningful or ethical one.

---

## 13. Connection to the project

Your project should not use classification simply because classification is this week's method.

Start from the project problem.

A reasonable sequence is:

**problem → target → observations → features → preprocessing → train/test split → baseline → classifier → evaluation → interpretation**

If your project does **not** have a meaningful categorical target, classification may not be the appropriate method.

For project work, ask:

> **Could our problem be expressed as predicting a meaningful category?**

If yes:

* What is the target?
* When would that target become known?
* Which features would already be known before that time?
* What information would create data leakage?
* Which error matters more?
* What baseline should the classifier beat?

If the answer is no, record that conclusion. Choosing **not** to use an unsuitable method is also part of correct data analysis.

---

# Minimal Classification Workflow

A first classification experiment can follow this structure:

1. Define the problem.
2. Define the target.
3. Select meaningful features.
4. Inspect class frequencies.
5. Split into training and test data.
6. Fit preprocessing only using training data.
7. Create a simple baseline.
8. Fit a classifier.
9. Predict test observations.
10. Examine the confusion matrix.
11. Calculate suitable metrics.
12. Interpret the errors in relation to the original problem.

The key principle is:

> **A high score does not make a model valid. The data, evaluation process and interpretation must also be valid.**

---

# Check Your Understanding

1. A dataset contains a numerical final grade from 0–100. Is predicting the exact grade a classification problem? What change would make it a classification problem?

2. A model achieves 96% accuracy, but 96% of the training examples belong to one class. What should you investigate before concluding that the model works well?

3. Why should missing-value imputation normally be fitted after the training/test split rather than before it?

4. A model has high precision but low recall. What kind of error is it making relatively often?

5. Your project dataset contains a variable recorded **after** the outcome you are trying to predict. Why could using that variable be a serious problem?

---

# Recommended Reading

For the conceptual classification methods, Zaki & Meira provide dedicated chapters on **probabilistic classification, decision trees and classification assessment**. ([Data Mining and Machine Learning][11])

For practical Python work, the **ISLP Classification Lab** provides current examples of train/test splitting, logistic regression, Naive Bayes and KNN. [ISLP – Classification Lab](https://intro-stat-learning.github.io/ISLP/labs/Ch04-classification-lab.html?utm_source=chatgpt.com)

VanderPlas provides accessible introductions to the scikit-learn workflow, Naive Bayes and decision trees/random forests. Some code in the original handbook uses older scikit-learn imports, so use the current course examples or current scikit-learn documentation when syntax differs. ([Pythonic Perambulations][12])

For the most important implementation rule this week, read the scikit-learn section on **data leakage and inconsistent preprocessing**. [scikit-learn – Common pitfalls and recommended practices](https://scikit-learn.org/stable/common_pitfalls.html?utm_source=chatgpt.com)

For evaluation, use the scikit-learn documentation on **classification metrics and confusion matrices**. [scikit-learn – Classification metrics](https://scikit-learn.org/stable/modules/model_evaluation.html?utm_source=chatgpt.com)


[1]: https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html?utm_source=chatgpt.com "LogisticRegression — scikit-learn 1.9.0 documentation"
[2]: https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.train_test_split.html?utm_source=chatgpt.com "train_test_split — scikit-learn 1.9.0 documentation"
[3]: https://intro-stat-learning.github.io/ISLP/labs/Ch04-classification-lab.html?utm_source=chatgpt.com "Logistic Regression, LDA, QDA, and KNN — Introduction to Statistical Learning (Python)"
[4]: https://scikit-learn.org/stable/modules/linear_model.html?utm_source=chatgpt.com "1.1. Linear Models — scikit-learn 1.9.0 documentation"
[5]: https://scikit-learn.org/stable/modules/generated/sklearn.dummy.DummyClassifier.html?utm_source=chatgpt.com "DummyClassifier — scikit-learn 1.9.0 documentation"
[6]: https://scikit-learn.org/stable/modules/model_evaluation.html?highlight=cross_val_score&utm_source=chatgpt.com "3.4. Metrics and scoring: quantifying the quality of predictions — scikit-learn 1.9.0 documentation"
[7]: https://scikit-learn.org/stable/modules/generated/sklearn.metrics.confusion_matrix.html?utm_source=chatgpt.com "confusion_matrix — scikit-learn 1.9.0 documentation"
[8]: https://scikit-learn.org/stable/common_pitfalls.html?highlight=linearregression&utm_source=chatgpt.com "11. Common pitfalls and recommended practices — scikit-learn 1.8.0 documentation"
[9]: https://scikit-learn.org/stable/modules/tree?utm_source=chatgpt.com "1.10. Decision Trees — scikit-learn 1.9.0 documentation"
[10]: https://jakevdp.github.io/PythonDataScienceHandbook/05.05-naive-bayes.html?utm_source=chatgpt.com "In Depth: Naive Bayes Classification | Python Data Science Handbook"
[11]: https://dataminingbook.info/book_html/?utm_source=chatgpt.com "Online Book | Data Mining and Machine Learning"
[12]: https://jakevdp.github.io/PythonDataScienceHandbook/?utm_source=chatgpt.com "Python Data Science Handbook | Python Data Science Handbook"
