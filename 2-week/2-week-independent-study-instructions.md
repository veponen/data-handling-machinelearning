# Week 2 Study Package

**Preparation for Monday 3: Classification**

Expected independent study time: **approximately 28 hours**

Suggested schedule: approximately **7 hours per day from Tuesday to Friday**.

This week follows the classification workflow:

**problem → target → features → train/test split → preprocessing → baseline → classifier → predictions → evaluation → interpretation**

The goal is not to learn many algorithms. The goal is to understand how to build and evaluate a classification solution correctly.

---

## Tuesday – Classification Concepts and scikit-learn

**Suggested time: ~7 h**

### 1. Course material – ~2 h

Study:

**Classification: From a Question to a Valid Prediction**

Focus especially on:

* classification vs regression and clustering;
* observations, features `X` and target `y`;
* binary and multiclass classification;
* training and test data;
* baseline models;
* prediction vs probability;
* confusion matrix;
* accuracy, precision and recall;
* data leakage;
* when classification is appropriate.

Complete the five **Check Your Understanding** questions at the end of the material.

### 2. scikit-learn workflow – ~2 h

Study selected parts of Jake VanderPlas:

[Introducing Scikit-Learn – Python Data Science Handbook](https://jakevdp.github.io/PythonDataScienceHandbook/05.02-introducing-scikit-learn.html?utm_source=chatgpt.com)

Concentrate on:

* features matrix `X`;
* target array `y`;
* estimator API;
* `fit()`;
* `predict()`;
* the Iris classification example.

The general scikit-learn workflow in this chapter is still useful, but some code uses older scikit-learn imports. Use the current course examples for implementation. ([Pythonic Perambulations][1])

### 3. Classification methods – ~2 h

Read selected parts of Zaki & Meira:

* Chapter 18: **Probabilistic Classification**

  * 18.1 Bayes Classifier
  * 18.2 Naive Bayes
  * 18.3 K Nearest Neighbors
* Browse Chapter 19: **Decision Tree Classifier**

Do not try to reproduce every mathematical derivation. Concentrate on:

* what the methods are trying to do;
* how observations are assigned to classes;
* assumptions;
* differences between the methods.

Zaki & Meira place probabilistic classification, KNN, decision trees and classification assessment in Chapters 18, 19 and 22. ([Data Mining and Machine Learning][2])

[Zaki & Meira – Online Book](https://dataminingbook.info/book_html/?utm_source=chatgpt.com)

### 4. Short practical check – ~1 h

In Jupyter:

1. Load a small classification dataset.
2. Identify `X` and `y`.
3. Inspect the target classes and their frequencies.
4. Split the data into training and test sets.
5. Fit one simple classifier.
6. Produce predictions.

Do not concentrate on model performance yet.

---

# Wednesday – Build a Classification Workflow

**Suggested time: ~7 h**

## Practical Exercise: First Classification Model

Work individually using the provided **synthetic classification dataset and notebook instructions**.

### Part A – Understand the problem

Before modelling, determine:

1. What does one observation represent?
2. What is the target?
3. Is the problem binary or multiclass?
4. Which variables could be useful features?
5. Which variables should not be features?
6. Are classes balanced?
7. What would a classification error mean?

### Part B – Prepare `X` and `y`

Create:

* feature matrix `X`;
* target `y`.

Inspect:

* missing values;
* categorical variables;
* numerical variables;
* variables that require preprocessing.

### Part C – Split before fitting

Create training and test sets.

Use a reproducible split and preserve class proportions where appropriate.

Example:

`train_test_split(..., stratify=y, random_state=...)`

The test set must remain unseen while the model and preprocessing are being fitted.

### Part D – Create a baseline

Use `DummyClassifier` or another clearly justified simple baseline.

A dummy classifier ignores the input features and provides a reference against which a real classifier can be compared. ([Scikit-learn][3])

Ask:

**Does our real model actually perform better than a trivial prediction?**

### Part E – Train classifiers

Train at least **two** actual classifiers.

Recommended choices:

* Logistic Regression
* Decision Tree

Optional:

* K Nearest Neighbors
* Naive Bayes

Do not search for the "best algorithm" yet.

Record:

* classifier used;
* important preprocessing;
* test accuracy;
* observations about the result.

---

# Thursday – Evaluation, Preprocessing and Leakage

**Suggested time: ~7 h**

## 1. Classification evaluation – ~2 h

Study the relevant parts of the scikit-learn documentation:

[Classification metrics and scoring](https://scikit-learn.org/stable/modules/model_evaluation.html?utm_source=chatgpt.com)

[Confusion matrix](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.confusion_matrix.html?utm_source=chatgpt.com)

Focus on:

* confusion matrix;
* true positive / false positive;
* true negative / false negative;
* accuracy;
* precision;
* recall;
* F1 score.

A confusion matrix records actual classes against predicted classes and lets you inspect the types of errors rather than relying on one overall score. ([Scikit-learn][4])

### Continue the practical exercise

For your classifiers:

1. calculate accuracy;
2. create a confusion matrix;
3. calculate precision and recall where appropriate;
4. compare results with the baseline;
5. identify the most important types of error.

Answer:

> Which model appears more useful for this problem, and why?

A slightly higher accuracy alone is not sufficient justification.

---

## 2. Data leakage and pipelines – ~2 h

Study:

[scikit-learn – Common pitfalls and recommended practices](https://scikit-learn.org/stable/common_pitfalls.html?utm_source=chatgpt.com)

Read especially:

* **Inconsistent preprocessing**
* **Data leakage**

Important rule:

**split first → fit preprocessing on training data → apply it to test data**

Do not let test information influence:

* scaling;
* missing-value imputation;
* feature selection;
* other learned preprocessing.

Scikit-learn specifically recommends pipelines because they help ensure that transformations are fitted only using the appropriate training data and applied consistently to test data. ([Scikit-learn][5])

### Practical work

Use a pipeline where appropriate.

Investigate at least one possible leakage problem:

* a variable recorded after the target;
* preprocessing fitted using all data;
* direct or indirect target information among the features.

Explain:

> Why would this make the model result unreliable?

---

## 3. Compare and interpret – ~2 h

Compare your models.

Create a small results table containing, where appropriate:

| Model | Baseline? | Accuracy | Precision | Recall | Main observation |
| ----- | --------- | -------: | --------: | -----: | ---------------- |

Then answer briefly:

1. Which model performed better than the baseline?
2. What mistakes does it make?
3. Is the dataset large enough to trust small differences between models?
4. Which result would you investigate further?
5. What limitation should be reported with the result?

---

## 4. Optional deeper practical reading – ~1 h

If you want more practical examples, use the ISLP classification lab:

[ISLP – Logistic Regression, LDA, QDA and KNN Lab](https://intro-stat-learning.github.io/ISLP/labs/Ch04-classification-lab.html?utm_source=chatgpt.com)

The lab contains practical examples of logistic regression, discriminant analysis, Naive Bayes and KNN. ([Intro Stat Learning][6])

You do not need to reproduce the entire lab.

---

# Friday – Project Connection and Preparation for Monday

**Suggested time: ~7 h**

## 1. Connect classification to your project – ~3 h

Work with your project group.

Do **not** assume that classification belongs in your project.

Discuss:

### Possible target

Could your project contain a meaningful categorical target?

If yes:

* What exactly would the target represent?
* When would it become known?

### Unit of analysis

What would one observation represent?

Examples might be:

* one student;
* one task attempt;
* one quiz attempt;
* one course week.

### Possible features

Which variables could be available **before** the target becomes known?

### Leakage

Which variables must not be used because they:

* directly reveal the target;
* occur after the prediction point;
* are calculated from the outcome?

### Applicability

Would classification actually help answer your project's problem?

If classification does not fit, state that clearly.

**Do not force classification into the project.**

Update your group's **Project Data Plan** with your conclusions.

---

## 2. Concept map – ~1.5 h

Prepare your individual Week 2 concept map.

Choose concepts you find important, difficult, surprising or strongly connected.

Possible concepts include:

* Classification
* Target
* Feature
* Training Data
* Test Data
* Baseline
* Prediction
* Probability
* Confusion Matrix
* Accuracy
* Precision
* Recall
* Data Leakage
* Pipeline

Do not try to include all of them.

Show meaningful relationships.

---

## 3. Preparation quiz – ~1 h

Complete the Week 2 theory quiz.

Topics may include:

* classification vs other ML tasks;
* features and target;
* binary and multiclass problems;
* train/test split;
* baseline;
* confusion matrix;
* accuracy;
* precision and recall;
* preprocessing;
* data leakage;
* appropriate use of classification.

---

## 4. Practical verification – ~0.5 h

Complete the practical verification task based on results from your notebook.

You may need values such as:

* number of observations;
* class distribution;
* test-set size;
* baseline result;
* confusion-matrix values;
* selected evaluation metrics.

---

## 5. Review and technical catch-up – ~1 h

Use the remaining time to:

* finish the notebook;
* correct technical problems;
* review unclear classification concepts;
* compare your results with your group;
* prepare questions for Monday.

---

# What to Submit Before Monday 3

This time the required returns are explicit.

### 1. Week 2 Classification Practical

**Individual – mandatory – PASS / REVISE / MISSING**

Submit your completed classification notebook.

It should show:

* problem and target;
* features;
* train/test split;
* preprocessing;
* baseline;
* at least two classifiers;
* confusion matrix and suitable metrics;
* interpretation;
* consideration of data leakage.

The teacher may ask you to explain or demonstrate any part of the work.

### 2. Week 2 Concept Map

**Individual – mandatory – PASS / REVISE / MISSING**

Submit your Week 2 concept map.

### 3. Week 2 Project Data Plan Update

**Group work**

Update the shared Project Data Plan with your classification discussion:

* possible target, if any;
* possible unit of analysis;
* candidate features;
* leakage risks;
* whether classification is appropriate for the project.

### 4. Week 2 Theory Quiz

Complete the automatically graded theory quiz.

### 5. Week 2 Practical Verification

Complete the automatically graded practical verification task.

---

# Ready for Monday 3

Before Monday you should be able to explain:

* when a problem is classification;
* what `X` and `y` represent;
* why training and test data are separated;
* why a baseline is needed;
* what a confusion matrix shows;
* the difference between accuracy, precision and recall;
* how preprocessing can cause data leakage;
* why a high model score alone does not prove that a model is useful.

You should also have built and evaluated at least one complete classification workflow yourself.

**Monday 3 will use this knowledge for deeper classification work and project support, not repeat the basic theory.**

[1]: https://jakevdp.github.io/PythonDataScienceHandbook/05.02-introducing-scikit-learn.html?utm_source=chatgpt.com "Introducing Scikit-Learn | Python Data Science Handbook"
[2]: https://dataminingbook.info/book_html/?utm_source=chatgpt.com "Online Book | Data Mining and Machine Learning"
[3]: https://scikit-learn.org/stable/modules/generated/sklearn.dummy.DummyClassifier.html?utm_source=chatgpt.com "DummyClassifier — scikit-learn 1.9.0 documentation"
[4]: https://scikit-learn.org/stable/modules/generated/sklearn.metrics.confusion_matrix.html?utm_source=chatgpt.com "confusion_matrix — scikit-learn 1.9.0 documentation"
[5]: https://scikit-learn.org/stable/common_pitfalls.html?highlight=linearregression&utm_source=chatgpt.com "11. Common pitfalls and recommended practices — scikit-learn 1.8.0 documentation"
[6]: https://intro-stat-learning.github.io/ISLP/labs/Ch04-classification-lab.html?utm_source=chatgpt.com "Logistic Regression, LDA, QDA, and KNN — Introduction to Statistical Learning (Python)"
