# Week 5 Study Package

**Preparation for Monday 6: Prediction of Numerical Values / Regression**

Expected independent study time: **approximately 28 hours**

Suggested schedule: approximately **7 hours per day from Tuesday to Friday**.

This week follows the regression workflow:

**problem → numerical target → features → train/test split → preprocessing → baseline → regression model → predictions → errors → validation → interpretation**

The goal is not to learn many regression algorithms. The goal is to understand how to build, evaluate and interpret a numerical prediction model correctly.

Regression is appropriate when the target is a **numerical value**.

Examples:

- next quiz score;
- task completion time;
- number of attempts;
- future activity count.

Classification predicts a category. Regression predicts a number.

---

# Tuesday – Regression Concepts and Linear Regression

**Suggested time: ~7 h**

## 1. Course introduction: numerical prediction – ~1.5 h

Before building a model, identify:

### Observation

What does one row represent?

Examples:

- one student;
- one student-week;
- one task attempt;
- one quiz attempt.

### Numerical target `y`

What number are we trying to predict?

Examples:

- score;
- duration;
- count;
- amount.

The target must have a meaningful numerical interpretation.

### Features `X`

Which variables are available when the prediction is supposed to be made?

This question is essential because information recorded after the prediction point can cause **data leakage**.

### Prediction error

For one observation:

`residual = actual value - predicted value`

A prediction of 75 for an actual value of 80 has a residual of:

`80 - 75 = 5`

A model should not be judged only by a few examples. We need measures that summarize prediction errors over many observations.

## 2. VanderPlas – Linear Regression – ~2 h

Study selected parts of:

**Jake VanderPlas – In Depth: Linear Regression**

https://jakevdp.github.io/PythonDataScienceHandbook/05.06-linear-regression.html

Focus especially on:

- simple linear regression;
- slope and intercept;
- `LinearRegression`;
- `fit()`;
- `predict()`;
- multiple linear regression;
- coefficients;
- the idea that several features can contribute to one numerical prediction.

Browse the sections on:

- polynomial features;
- ridge regression;
- lasso regression.

You do not need to reproduce all mathematical derivations.

Important idea:

> A linear regression model can use several features even though we cannot easily draw the model in two dimensions.

## 3. Zaki & Meira – Linear Regression – ~2 h

Study selected parts of:

**Zaki & Meira – Chapter 23: Linear Regression**

https://dataminingbook.info/book_html/

Focus on:

- 23.1 Linear Regression Model;
- 23.2 Bivariate Regression;
- 23.3 Multiple Regression.

Browse:

- 23.4 Ridge Regression.

Concentrate on:

- what the model predicts;
- relationship between features and numerical target;
- coefficients;
- fitting a model from data;
- why more features do not automatically produce a better model.

Do not concentrate on deriving the equations by hand.

## 4. Short practical check – ~1.5 h

In Jupyter:

1. Create or load a small dataset with one numerical target.
2. Identify `X` and `y`.
3. Split the data into training and test sets.
4. Fit `LinearRegression`.
5. Produce test-set predictions.
6. Compare several actual and predicted values.
7. Calculate residuals.

Make a simple scatter plot of:

**actual value vs predicted value**

Do not concentrate on optimizing the model yet.

---

# Wednesday – Build a Regression Workflow

**Suggested time: ~7 h**

## Practical Exercise: Predict a Numerical Value

Work individually in Jupyter using:

**`synthetic-regression-dataset.csv`**

The purpose is to build, compare and interpret a complete numerical-prediction workflow.

## Part A – Understand the prediction problem

Before modelling, determine:

1. What does one observation represent?
2. What is the numerical target?
3. At what point should the prediction be made?
4. Which variables exist before that prediction point?
5. Which variables would reveal future information?
6. Which variables are identifiers?
7. Are there missing values?
8. What would a large prediction error mean in this problem?

Write the answers briefly in the notebook.

## Part B – Create `X` and `y`

Create:

- feature matrix `X`;
- numerical target `y`.

Inspect:

- numerical variables;
- categorical variables;
- missing values;
- identifiers;
- variables that need preprocessing;
- possible leakage variables.

Do not use a feature simply because it is available in the file.

Ask:

> Would this information genuinely be available when the prediction is made?

## Part C – Split before fitting

Create training and test sets.

Use a reproducible split.

For example:

`train_test_split(..., test_size=0.25, random_state=...)`

Remember:

> The test set must remain unseen while the model and learned preprocessing are fitted.

If preprocessing learns something from the data, fit it using the training data only.

Use a pipeline where appropriate.

## Part D – Create a baseline

Use:

`DummyRegressor(strategy="mean")`

This model always predicts the mean target value learned from the training data.

The baseline asks:

> Does our real regression model actually predict better than simply using a typical value?

Record baseline results.

## Part E – Fit a linear regression model

Fit:

`LinearRegression()`

Produce test-set predictions.

Inspect:

- several actual values;
- corresponding predicted values;
- residuals;
- model coefficients.

Do not interpret a coefficient without considering:

- what the feature means;
- its units;
- other features in the model;
- whether the relationship is plausibly linear.

## Part F – Compare with another regression model

Fit one additional model.

Recommended:

`Ridge()`

Ridge regression is still a linear model but adds regularization that discourages very large coefficients.

Compare:

- DummyRegressor;
- LinearRegression;
- Ridge.

The goal is not to find a universal "best model".

The goal is to understand whether modelling adds useful predictive information and how model choices affect results.

---

# Thursday – Prediction Errors, Validation and Model Comparison

**Suggested time: ~7 h**

## 1. Regression evaluation – ~2 h

Study the regression metrics in current scikit-learn documentation:

https://scikit-learn.org/stable/modules/model_evaluation.html

Concentrate on:

- Mean Absolute Error (**MAE**);
- Root Mean Squared Error (**RMSE**);
- coefficient of determination (**R²**).

### MAE

MAE is the average absolute prediction error.

It remains in the same unit as the target.

If:

`MAE = 5.4`

and the target is quiz percentage points, the model is wrong by about **5.4 percentage points on average**.

### RMSE

RMSE also uses the target's unit, but larger errors influence it more strongly than they influence MAE.

Compare MAE and RMSE.

Ask:

> Are a few large errors important in this problem?

### R²

R² measures predictive performance relative to a constant reference based on the target mean.

Important:

- `R² = 1` is perfect prediction;
- `R² = 0` means performance comparable to the reference under the usual definition;
- `R² < 0` is possible and indicates worse performance than that reference.

Do **not** interpret R² as an "accuracy percentage".

## 2. Evaluate your models – ~1.5 h

For:

- DummyRegressor;
- LinearRegression;
- Ridge;

calculate:

- MAE;
- RMSE;
- R².

Create a table:

| Model | MAE | RMSE | R² | Main observation |
|---|---:|---:|---:|---|
| DummyRegressor | | | | |
| LinearRegression | | | | |
| Ridge | | | | |

Then answer:

1. Which models beat the baseline?
2. Is the difference large enough to matter?
3. Which metric is most understandable in the target's real unit?
4. Are there unusually large errors?

## 3. Residuals and visualization – ~1.5 h

Create at least two useful visualizations.

### Actual vs predicted

Plot:

- actual target values;
- predicted target values.

A perfect model would place observations on the line where:

`predicted = actual`

### Residual plot

Plot residuals against predicted values.

Investigate:

- systematic overprediction;
- systematic underprediction;
- increasing error for large target values;
- unusual observations;
- patterns suggesting that a straight-line model is insufficient.

Ask:

> Are the errors random-looking, or is the model systematically missing something?

## 4. Validation and split sensitivity – ~1.5 h

A result from one train/test split is not automatically stable.

Repeat the experiment using several reasonable random splits.

Compare:

- MAE;
- RMSE;
- R².

Ask:

> Does the conclusion change substantially when the split changes?

### Repeated observations warning

If the dataset contains several rows from the same student, a random row split may place observations from the same person in both training and test sets.

That can make evaluation more optimistic because training and test observations are not fully independent.

For project data, always ask:

> Should the split be by rows, by student, or by time?

The correct choice depends on the prediction problem.

## 5. Data leakage – ~0.5 h

Return to the scikit-learn guidance on common pitfalls:

https://scikit-learn.org/stable/common_pitfalls.html

Important rule:

**split first → fit preprocessing/model on training data → evaluate on unseen data**

Also check for features that:

- happen after the target;
- directly contain the target;
- are calculated using later information.

A model with suspiciously excellent results deserves investigation.

---

# Friday – Project Connection and Preparation for Monday

**Suggested time: ~7 h**

## 1. Connect regression to your project – ~3 h

Work with your project group.

Do **not** assume that regression belongs in your project.

### Numerical target

Could your project contain a meaningful numerical target?

Examples:

- future score;
- duration;
- attempt count;
- activity count.

Ask:

> Is predicting this value actually useful for our project problem?

### Prediction point

When should the prediction be made?

This must be defined before choosing features.

### Unit of analysis

What does one observation represent?

Examples:

- one student;
- one student-week;
- one task attempt;
- one quiz attempt.

### Features

Which variables are available **before** the target becomes known?

### Leakage

Which variables must not be used because they:

- occur after the prediction point;
- directly reveal the target;
- are derived from the target;
- use future information.

### Validation

Would rows from the same student appear multiple times?

Would a random row split be appropriate?

Could a time-based or student-based split be more defensible?

### Error meaning

Suppose the MAE is 5.

Is an average error of 5 units:

- small;
- acceptable;
- too large?

That depends on what the target represents.

### Applicability

Would numerical prediction genuinely help the project?

If not, state that clearly.

**Do not force regression into the project.**

Update your group's **Project Data Plan** with your conclusion.

## 2. Concept map – ~1.5 h

Prepare your individual Week 5 concept map.

Choose concepts you find important, difficult, surprising or strongly connected.

Possible concepts include:

- Regression
- Numerical Target
- Feature
- Prediction
- Linear Regression
- Coefficient
- Intercept
- Residual
- Train/Test Split
- Baseline
- DummyRegressor
- MAE
- RMSE
- R²
- Ridge Regression
- Validation
- Data Leakage
- Prediction Point

Do not try to include all of them.

Show meaningful relationships.

## 3. Preparation quiz – ~1 h

Complete the Week 5 theory quiz.

Topics may include:

- regression vs classification;
- numerical target;
- observations and features;
- linear regression;
- coefficients and intercept;
- baseline regression;
- predictions and residuals;
- MAE;
- RMSE;
- R²;
- train/test split;
- model comparison;
- validation;
- repeated observations;
- data leakage;
- appropriate use of regression.

## 4. Practical verification – ~0.5 h

Complete the practical verification task based on your notebook.

You may need values such as:

- number of observations;
- selected target;
- number of features;
- train/test sizes;
- baseline MAE;
- model MAE;
- RMSE;
- R²;
- selected model comparison result.

## 5. Review and technical catch-up – ~1 h

Use the remaining time to:

- finish the notebook;
- correct technical problems;
- review unclear regression concepts;
- compare findings with your group;
- prepare questions for Monday.

---

# What to Submit Before Monday 6

## 1. Week 5 Regression Practical

**Individual – mandatory – PASS / REVISE / MISSING**

Submit your completed Jupyter notebook.

It should show:

- definition of the prediction problem;
- unit of analysis;
- numerical target;
- prediction point;
- feature selection;
- consideration of leakage;
- preprocessing;
- train/test split;
- DummyRegressor baseline;
- LinearRegression;
- Ridge regression;
- predictions and residuals;
- MAE;
- RMSE;
- R²;
- actual-vs-predicted visualization;
- residual visualization;
- comparison of several train/test splits;
- interpretation and limitations.

The teacher may ask you to explain or demonstrate any part of the work.

## 2. Week 5 Concept Map

**Individual – mandatory – PASS / REVISE / MISSING**

Submit your Week 5 concept map.

## 3. Week 5 Project Data Plan Update

**Group work**

Update the shared Project Data Plan with your regression discussion:

- possible numerical target;
- prediction point;
- unit of analysis;
- possible features;
- leakage risks;
- suitable validation split;
- meaning of prediction errors;
- whether regression is appropriate for the project.

## 4. Week 5 Theory Quiz

Complete the automatically graded theory quiz.

## 5. Week 5 Practical Verification

Complete the automatically graded practical verification task.

---

# Ready for Monday 6

Before Monday you should be able to explain:

- when regression is appropriate;
- how regression differs from classification;
- what a numerical target is;
- why the prediction point must be defined;
- what a linear regression model does;
- what coefficients and intercept represent at a basic level;
- why a baseline model is needed;
- what a residual is;
- what MAE tells you;
- why RMSE reacts strongly to large errors;
- why R² is not an accuracy percentage;
- why one train/test split may not be enough;
- why repeated observations can affect validation;
- how data leakage can produce unrealistically good results;
- why the most accurate-looking model is not automatically the most useful one.

You should also have built, compared and interpreted a complete numerical-prediction workflow yourself.

**Monday 6 will use this knowledge for deeper regression, validation and project work rather than repeat the basic theory.**

---

# Source links

- VanderPlas – In Depth: Linear Regression:
  https://jakevdp.github.io/PythonDataScienceHandbook/05.06-linear-regression.html

- Zaki & Meira – Online Book:
  https://dataminingbook.info/book_html/

- scikit-learn – Metrics and scoring:
  https://scikit-learn.org/stable/modules/model_evaluation.html

- scikit-learn – Common pitfalls and recommended practices:
  https://scikit-learn.org/stable/common_pitfalls.html

- scikit-learn – DummyRegressor:
  https://scikit-learn.org/stable/modules/generated/sklearn.dummy.DummyRegressor.html

- Optional: ISLP – Linear Regression Lab:
  https://intro-stat-learning.github.io/ISLP/labs/Ch03-linreg-lab.html
