# Week 7 Study Package

**Preparation for Monday 8: Validation, Visualization and Conclusions**

Expected independent study time: **approximately 28 hours**

Suggested schedule: approximately **7 hours per day from Tuesday to Friday**.

This is the final theory-focused independent-study week.

The goal is to bring the course together:

**problem → method choice → validation → visualization → interpretation → limitations → conclusions → communication**

You are not learning another new algorithm this week.

Instead, you will check whether your analysis is valid, understandable and useful.

---

# Tuesday – Validation Across the Course

**Suggested time: ~7 h**

## Study sources

Use these before/during Tuesday's work:

1. **Jake VanderPlas – Hyperparameters and Model Validation**  
   https://jakevdp.github.io/PythonDataScienceHandbook/05.03-hyperparameters-and-model-validation.html  
   Focus on holdout sets, cross-validation and why evaluation on training data is misleading.

2. **scikit-learn – Metrics and scoring: quantifying the quality of predictions**  
   https://scikit-learn.org/stable/modules/model_evaluation.html  
   Review the sections relevant to **classification, regression and clustering**. You do not need to study every metric.

3. **scikit-learn – Common pitfalls and recommended practices**  
   https://scikit-learn.org/stable/common_pitfalls.html  
   Focus especially on **inconsistent preprocessing** and **data leakage**.

4. **Optional deeper study: ISLP – Cross-Validation and the Bootstrap**  
   https://intro-stat-learning.github.io/ISLP/labs/Ch05-resample-lab.html

Also use your earlier course materials from classification, clustering, association analysis and regression when reviewing method-specific validation.

## 1. What does validation mean? – ~1.5 h

Validation asks:

> **Can we trust the result for the purpose we care about?**

A good-looking result is not enough.

You must ask:

- Was the right target or question used?
- Was the data suitable?
- Was the evaluation designed correctly?
- Is there leakage?
- Does the result generalize?
- Is the result stable?
- Does the metric match the real problem?

Validation depends on the method.

---

## 2. Classification validation – ~1 h

Review:

- baseline;
- train/test split;
- confusion matrix;
- accuracy;
- precision;
- recall;
- F1 score;
- class imbalance;
- leakage.

Ask:

> Which errors matter most?

A higher accuracy does not automatically mean a better solution.

---

## 3. Regression validation – ~1 h

Review:

- baseline;
- MAE;
- RMSE;
- R²;
- residuals;
- repeated observations;
- row split vs student split vs time split;
- leakage.

Ask:

> Are the errors acceptable in the original target unit?

---

## 4. Clustering validation – ~1 h

Clustering usually has no known target.

Therefore validation is different.

Review:

- scaling;
- cluster stability;
- sensitivity to parameters;
- visual separation;
- whether clusters are interpretable;
- whether clusters are actually useful.

Important:

> A cluster is a mathematical grouping, not automatically a meaningful real-world category.

Do not label people as fixed "types" simply because an algorithm placed them in a cluster.

---

## 5. Association-analysis validation – ~1 h

Review:

- support;
- confidence;
- lift;
- minimum thresholds;
- structural or obvious rules;
- association vs causation.

Ask:

- Is the rule frequent enough to matter?
- Does it add information beyond the commonness of the consequence?
- Is the rule simply caused by how the data were constructed?

---

## 6. Short validation exercise – ~1.5 h

Choose **two analyses** you have completed during the course.

For each, write:

1. What question was the analysis trying to answer?
2. What was the unit of analysis?
3. Which method was used?
4. What result looked strongest?
5. What could make that result misleading?
6. What additional check would increase your confidence?

Keep the answers short.

---

# Wednesday – Visualization for Understanding and Communication

**Suggested time: ~7 h**

## Study sources

Use selected parts of **Jake VanderPlas – Python Data Science Handbook, Chapter 4: Visualization with Matplotlib**:

Main chapter index:  
https://jakevdp.github.io/PythonDataScienceHandbook/

Especially:

- **Simple Scatter Plots**  
  https://jakevdp.github.io/PythonDataScienceHandbook/04.02-simple-scatter-plots.html
- **Visualizing Errors**  
  https://jakevdp.github.io/PythonDataScienceHandbook/04.03-errorbars.html
- **Histograms, Binnings, and Density**  
  https://jakevdp.github.io/PythonDataScienceHandbook/04.05-histograms-and-binnings.html

Do not try to learn every Matplotlib option. Concentrate on choosing a plot that answers the analytical question and presenting it clearly.

## 1. Why visualize? – ~1 h

Visualization has at least two purposes:

### Understand the data

Use plots to investigate:

- distributions;
- missing values;
- outliers;
- relationships;
- groups;
- errors.

### Communicate results

Use plots to explain:

- what happened;
- what the model found;
- how large the effect or error is;
- why the result matters.

A plot should answer a question.

---

## 2. Choose the plot from the question – ~1.5 h

Examples:

### Distribution of one numerical variable

Possible plots:

- histogram;
- box plot.

### Compare a numerical variable between categories

Possible plots:

- box plot;
- grouped summary chart.

### Relationship between two numerical variables

Possible plots:

- scatter plot.

### Classification performance

Possible plots:

- confusion matrix;
- class-wise metric chart.

### Regression performance

Possible plots:

- actual vs predicted;
- residual plot.

### Clustering

Possible plots:

- scatter plot when suitable dimensions exist;
- reduced-dimension visualization with caution.

### Association analysis

Possible presentations:

- compact rule table;
- support/confidence/lift comparison;
- carefully designed network view for a small number of rules.

Do not add a plot simply because a library makes it easy.

---

## 3. Avoid misleading visualizations – ~1 h

Check:

- axis ranges;
- units;
- labels;
- category order;
- excessive precision;
- hidden missing values;
- tiny groups;
- 3D effects that distort comparisons;
- too many colours or categories;
- a plot that suggests causation when only association was measured.

Ask:

> What could a reader misunderstand from this figure?

---

## 4. Practical visualization task – ~2 h

Use your group project data or results.

Create at least **three candidate figures**.

They should serve different purposes, for example:

1. understand the data;
2. show the main analysis result;
3. show a limitation, error or uncertainty.

For each figure, write one sentence:

> **What should the reader learn from this figure?**

Then remove any figure that does not have a clear purpose.

---

## 5. Improve one figure – ~1.5 h

Choose your most important project figure.

Check:

- clear title;
- meaningful axis names;
- units;
- readable category names;
- unnecessary elements removed;
- no misleading scale;
- short caption or interpretation.

Aim for:

> **one figure → one main message**

---

# Thursday – Method Choice, Limitations, Ethics and Conclusions

**Suggested time: ~7 h**

## Study sources

For **method choice and applicability**, review the relevant sections of your earlier weekly study packages. The purpose now is to compare methods you have already used, not learn another algorithm.

For **privacy and legal constraints**, read:

1. **European Commission – Principles of the GDPR**  
   https://commission.europa.eu/law/law-topic/data-protection/information-business-and-organisations/principles-gdpr_en  
   Focus on purpose limitation, data minimisation, accuracy, storage limitation, integrity/confidentiality and accountability.

2. **European Commission – Application of the GDPR**  
   https://commission.europa.eu/law/law-topic/data-protection/information-business-and-organisations/application-gdpr_en  
   Focus on what counts as personal data and the difference between pseudonymised and genuinely anonymous data.

3. **Optional current context: European Commission – AI Act**  
   https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai  
   Read the overview and risk-based approach. You do not need to learn the legislation in detail.

The goal is not to become a lawyer. You should be able to recognize when data processing or automated conclusions require additional privacy, legal or ethical consideration.

## 1. Choose methods from the problem – ~1.5 h

Review the main course methods:

### Classification

Use when the target is categorical.

### Regression

Use when the target is numerical.

### Clustering

Use when you want to investigate possible groups without a target.

### Association analysis

Use when you want to investigate co-occurrence or rule-like relationships.

### NLP

Use when text is an important part of the data or problem.

The first question is not:

> Which algorithm do I want to use?

The first question is:

> What problem am I trying to solve?

---

## 2. Applicability check – ~1 h

For your project, answer:

1. What is the actual problem?
2. What decision or understanding should the analysis support?
3. What is the unit of analysis?
4. Which method was selected?
5. Why does that method fit the problem?
6. Which method would **not** fit, and why?

It is acceptable to conclude that a simpler descriptive analysis is more appropriate than machine learning.

---

## 3. Limitations – ~1.5 h

Every project should state limitations.

Possible limitations include:

- small dataset;
- synthetic data;
- missing values;
- repeated observations;
- noisy labels;
- unclear measurement;
- class imbalance;
- possible leakage;
- unstable clusters;
- arbitrary thresholds;
- limited time period;
- model assumptions;
- uncertain generalization;
- data collected for another purpose.

Do not write:

> "There are no limitations."

Instead ask:

> **What should a reader know before trusting or using this result?**

---

## 4. Ethics, privacy and legal constraints – ~1.5 h

Review your project data and possible use.

Ask:

- Is every variable actually needed?
- Could someone be identified from the data?
- Does the data contain sensitive information?
- Is text being used?
- Could the model unfairly label an individual?
- Are inferred variables being treated as facts?
- Could the analysis be used for a purpose different from the reason the data were collected?
- Would a human review be required before acting on the result?

For educational data in particular:

> system activity is not the same as motivation, effort, ability or physical attendance.

Do not make stronger claims than the measurement supports.

---

## 5. From result to conclusion – ~1.5 h

A good conclusion connects:

**question → evidence → interpretation → limitation**

Example structure:

> We investigated whether X was related to Y.  
> The analysis showed ...  
> This suggests ...  
> However, the result should be interpreted cautiously because ...

Avoid:

- claiming causation from association;
- presenting a model score without interpretation;
- claiming the model is "good" without comparison;
- generalizing far beyond the data;
- hiding weak or contradictory results.

---

# Friday – Final Project Analysis Review

**Suggested time: ~7 h**

## Sources for Friday

No new theory source is required.

Use:

- the Tuesday–Thursday readings;
- your previous weekly study packages;
- your own project notebook/data/results;
- feedback and findings from earlier Monday sessions.

Friday is for applying the course material to the final project analysis.

Work mainly with your group project.

This is **not yet the final project submission**.

The purpose is to make sure the analysis is ready for Monday 8 and for final completion afterward.

---

## 1. Final analysis checklist – ~2 h

Review your project from the beginning.

### Problem

- Is the problem stated clearly?
- Is the question answerable with the available data?

### Data

- Is the unit of analysis clear?
- Are important variables explained?
- Are missing values and data-quality issues described?

### Method

- Does the chosen method fit the problem?
- Is preprocessing justified?
- Is the method described briefly and correctly?

### Validation

- Is there a baseline where appropriate?
- Is the split/evaluation strategy appropriate?
- Are useful metrics reported?
- Have you checked leakage?

### Visualization

- Do figures answer clear questions?
- Are axes, units and labels understandable?
- Are misleading presentations avoided?

### Interpretation

- What is the strongest result?
- What is uncertain?
- What should not be concluded?

### Limitations

- Are the main limitations stated?

### Ethics and privacy

- Are there variables or interpretations that should not be used?
- Are conclusions proportional to the evidence?

---

## 2. Prepare the project result story – ~2 h

Prepare a short explanation of your project using this structure:

1. **Problem**
2. **Data**
3. **Method**
4. **Main result**
5. **Validation**
6. **Visualization**
7. **Limitation**
8. **Conclusion**

Aim for clarity.

Do not describe every technical step.

---

## 3. Concept map – ~1.5 h

Prepare your individual Week 7 concept map.

Possible concepts:

- Validation
- Baseline
- Train/Test Split
- Leakage
- Generalization
- Stability
- Metric
- Residual
- Confusion Matrix
- Visualization
- Interpretation
- Applicability
- Limitation
- Uncertainty
- Ethics
- Privacy
- Conclusion
- Communication

Do not try to include all of them.

Show meaningful relationships.

---

## 4. Preparation quiz – ~1 h

Complete the Week 7 theory quiz.

Topics may include:

- validation across different ML methods;
- baseline comparison;
- leakage;
- split strategy;
- interpretation of metrics;
- choosing appropriate visualizations;
- misleading visualizations;
- method applicability;
- limitations;
- ethics and privacy;
- communicating conclusions.

---

## 5. Practical verification – ~0.5 h

Complete the Week 7 practical verification.

This verification may use short scenarios rather than one fixed dataset.

You may need to identify:

- appropriate validation method;
- suitable visualization;
- possible leakage;
- misleading interpretation;
- relevant limitation;
- appropriate conclusion.

---

# What to Submit Before Monday 8

## 1. Week 7 Final Analysis Review

**Group work**

Submit or update your project analysis so that it clearly includes:

- problem;
- unit of analysis;
- chosen method;
- validation;
- main result;
- at least one useful visualization;
- interpretation;
- limitations;
- ethical/privacy considerations;
- current conclusion.

This does **not** replace the final project submission.

---

## 2. Week 7 Concept Map

**Individual – mandatory – PASS / REVISE / MISSING**

Submit the Week 7 concept map.

---

## 3. Week 7 Theory Quiz

Complete the automatically graded theory quiz.

---

## 4. Week 7 Practical Verification

Complete the automatically graded practical verification.

---

# Ready for Monday 8

Before Monday you should be able to explain:

- why validation depends on the method and real use case;
- why a baseline matters;
- how leakage can invalidate a result;
- why train/test strategy matters;
- how to choose a visualization from the question;
- how a visualization can mislead;
- why method choice starts from the problem;
- how to state limitations;
- why association does not prove causation;
- why educational activity data should not be interpreted as direct measures of motivation or ability;
- how to connect evidence, interpretation, limitation and conclusion.

You should also have your group project analysis in a state where it can be reviewed, discussed and improved during Monday 8.

**Monday 8 will focus on validation, visualization, conclusions and project support. After Monday, the remaining independent work is final project completion and submission.**
