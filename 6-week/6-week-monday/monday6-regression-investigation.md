# Monday 6 – Regression Investigation

Use your Week 5 regression notebook and `synthetic-regression-dataset.csv`.

This is **not a repeat of the self-study practical**.

The self-study task was about building a complete regression workflow.  
This Monday task is about understanding **one result or modelling choice more deeply**.

## Your task

Choose **one** question to investigate.

Use this structure:

**Question → experiment → evidence → interpretation**

Possible questions:

- Does `LinearRegression` clearly beat `DummyRegressor`?
- Does `Ridge` change the result?
- Why is RMSE larger than MAE?
- Which observations have the largest residuals?
- Does the model systematically overpredict or underpredict?
- What happens when you change `random_state`?
- What happens if you remove one feature?
- What happens if you use a student-based split instead of a random row split?
- What happens if you use a time-based split?
- What happens if you incorrectly include `next_week_quiz_grade_0_5` as a feature?
- Is the model result actually useful for the problem?

You may also choose another regression question from your own notebook.

## What to do

### 1. State the question

Write one clear question.

Example:

> Does a random row split give a more optimistic result than a student-based split?

### 2. Run an experiment

Change **one relevant thing** and rerun the analysis.

Keep the comparison understandable.

### 3. Show evidence

Use appropriate evidence, for example:

- MAE;
- RMSE;
- R²;
- residuals;
- actual vs predicted plot;
- residual plot;
- small comparison table.

Do not report only one number if the question needs more evidence.

### 4. Interpret

Write a short conclusion:

- What changed?
- Why might it have changed?
- Does the result affect how much you trust the model?
- What limitation remains?

## Group discussion

Compare your investigation with your group.

Be ready to share:

1. your question;
2. the most important evidence;
3. one conclusion or remaining question.

## Important

A better metric value does not automatically mean a better model.

Always ask:

> **What are we predicting? When? Using what information? How wrong are we? Can we trust the evaluation?**
