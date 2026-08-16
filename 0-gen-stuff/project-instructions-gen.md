# Data Handling and Machine Learning – Group Project Instructions

## 1. Purpose of the project

The purpose of the group project is to practice a complete data handling and machine learning workflow using a realistic data-producing system.

All projects are based on the **Education / Learning Analytics** domain. You will work with data structures based on the Edge-LMS learning management system.

The main goal is not simply to train a machine learning model. You are expected to understand:

* how the original data is produced,
* how raw data is transformed into an analytical dataset,
* how artificial data can be created responsibly,
* how an appropriate machine learning problem is formulated,
* how models are evaluated,
* and how the results should be interpreted.

Different groups will investigate different problems using the same general domain and similar underlying data structures.

---

## 2. Project allocation

Each group will initially receive a project topic randomly.

A limited number of additional project topics will be available as alternatives.

Before the announced project-selection deadline, groups may:

* exchange project topics with another group, or
* return their assigned topic to the available project pool and select an available alternative topic.

After the deadline, project topics are fixed.

Each group is responsible for completing the project topic it holds after the deadline.

---

## 3. Your project problem

Your group will receive a separate **Project Card** describing the problem you are expected to investigate.

The Project Card defines the main problem, but it does not prescribe the exact solution.

Your group must make justified decisions concerning:

* how to represent the problem using data,
* what information is relevant,
* how to prepare the data,
* what machine learning methods to investigate,
* how to evaluate the results,
* and how to interpret the outcome.

The goal is therefore not to find one predetermined correct model.

---

## 4. The common data environment

The projects use a simplified file-based data structure based on Edge-LMS.

The available data may represent information such as:

* students,
* courses,
* modules,
* quiz questions,
* quiz attempts,
* quiz results,
* course progress,
* and LMS activity events.

You will receive documentation describing the relevant files, fields and relationships.

Not every project needs every available data source.

One of your first tasks is to determine which raw data is useful for your particular project.

---

## 5. Stage 1 – Generate and inspect real system data

You will use Edge-LMS yourself and generate a small amount of actual system data through normal interaction with the system.

For example, you may:

* log in,
* access course material,
* complete quizzes,
* make several quiz attempts,
* obtain different scores,
* progress between modules,
* and create normal LMS activity events.

You should inspect how these actions appear in the underlying data files.

The purpose of this stage is to understand how actions in an information system become data.

The small amount of data produced by your group is **not expected to be sufficient for machine learning**.

---

## 6. Stage 2 – Create artificial data

Your group must create a larger artificial dataset suitable for your project.

The artificial data should follow the provided Edge-LMS data structure sufficiently closely that the same data-handling methods could also be applied to equivalent real data.

Do not generate data as completely independent random numbers.

Your artificial dataset should contain documented assumptions and relationships.

For example:

* students with stronger earlier performance might have a higher probability of succeeding in later quizzes,
* difficult questions might produce more unsuccessful attempts,
* some students might study regularly while others work in short intensive periods,
* some students might stop progressing through the course,
* some data might deliberately be missing,
* unusual LMS events might occur rarely.

The assumptions should be appropriate for your specific project problem.

---

## 7. Document your artificial data assumptions

Your group must describe how the artificial data was generated.

Document at least:

* the number and types of records generated,
* the important variables,
* the important relationships between variables,
* probability or rule-based assumptions used,
* deliberately introduced noise,
* missing data or anomalies,
* and any important simplifications.

This is important because artificial data gives you something that is rarely available with real-world data:

**you know how the data was generated.**

Later you can investigate whether your analysis and machine learning methods are able to discover the patterns you deliberately created.

---

## 8. Stage 3 – Build an analytical dataset

Raw system data is normally not directly suitable for machine learning.

You must transform the raw data into an analytical dataset appropriate for your project.

Depending on the project, one analytical observation might represent:

* one student,
* one quiz attempt,
* one quiz question,
* one course module,
* one activity period,
* or another meaningful unit.

You may need to combine information from several files.

Typical tasks may include:

* joining data,
* filtering records,
* aggregating events,
* handling timestamps,
* calculating summary variables,
* handling missing values,
* identifying invalid records,
* encoding categorical variables,
* scaling numerical variables,
* and constructing new features.

You must be able to explain how your analytical dataset was constructed from the original data.

---

## 9. Explore the data

Before building machine learning models, investigate the data.

Your exploratory analysis should help you understand:

* distributions,
* typical values,
* unusual values,
* missing information,
* relationships between variables,
* class balance,
* and potential problems in the dataset.

Use appropriate statistics and visualizations.

Exploration should be connected to your project problem. Avoid producing graphs simply because they are easy to create.

---

## 10. Define the machine learning task

Translate your project problem into a clear analytical or machine learning task.

Depending on the project, this may involve:

* classification,
* regression,
* clustering,
* anomaly detection,
* or another suitable analytical approach.

Clearly identify, where applicable:

* the unit of observation,
* input features,
* prediction target,
* prediction point,
* and evaluation criteria.

Be particularly careful that your model does not use information that would not actually be available at the time a prediction is supposed to be made.

---

## 11. Establish a baseline

Before using more advanced methods, establish a simple baseline.

A baseline may be:

* predicting the majority class,
* predicting an average value,
* using a simple rule,
* or using a simple statistical or machine learning model.

A more complicated model is useful only if it provides meaningful improvement over a reasonable baseline.

---

## 12. Build and compare models

Investigate suitable machine learning approaches for your problem.

You are not expected to try every available algorithm.

It is normally better to investigate a small number of sensible alternatives and understand them properly.

Your group should be able to explain:

* why the methods were selected,
* what preprocessing they require,
* what important parameters were used,
* and what differences you observed between the methods.

---

## 13. Evaluate the results

Use evaluation methods appropriate for your particular problem.

Do not rely only on a single accuracy number.

Depending on the project, useful measures might include:

* accuracy,
* precision,
* recall,
* F1 score,
* confusion matrix,
* MAE,
* RMSE,
* other suitable error measures,
* cluster quality measures,
* or analysis of detected anomalies.

Where appropriate, separate training and evaluation data correctly.

Explain what the evaluation results mean in the context of the original project problem.

---

## 14. Analyze errors and limitations

Machine learning results should not be treated as automatically correct.

Investigate situations where your model performs poorly.

Consider questions such as:

* Which observations are difficult?
* Are some groups of observations systematically misclassified?
* Does performance change when the data becomes noisier?
* Does class imbalance affect the result?
* Are important variables missing?
* Could information leakage be present?
* Would the model work with real data as well as with your artificial data?

Discuss important limitations openly.

---

## 15. Interpret the model

Where appropriate, investigate what information the model appears to use.

For example:

* which features seem important,
* what relationships appear in the data,
* what distinguishes discovered clusters,
* or why particular cases are considered anomalous.

Be careful when interpreting these relationships.

A variable being useful for prediction does **not** necessarily mean that it causes the predicted outcome.

---

## 16. Compare your findings with your artificial-data assumptions

Because you created part of the dataset yourself, compare your results against the known data-generation process.

Ask:

* Did the analysis find relationships that were intentionally created?
* Did the model miss any important relationships?
* Did it appear to find relationships that were not deliberately created?
* How did random variation affect the results?
* Could misleading conclusions be drawn from the dataset?

This comparison is an important part of the project.

---

## 17. Ethics and responsible use

Learning analytics can involve information about individual students.

Consider the responsible use of your results.

Depending on the project, discuss issues such as:

* privacy,
* inappropriate profiling,
* fairness,
* false positive and false negative decisions,
* automated decision-making,
* and how predictions should be communicated to teachers or students.

The project dataset should primarily use the artificial data created for the exercise.

Do not build your project around the personal behaviour of identifiable classmates.

---

## 18. Reproducibility

Another person should be able to understand how your results were produced.

Keep your project organized.

Your work should make clear:

* where the raw data comes from,
* how artificial data is generated,
* how data preparation is performed,
* how the analytical dataset is created,
* how models are trained,
* and how results are evaluated.

Where practical, data generation and preprocessing should be reproducible by running your code again.

Use a fixed random seed where this is useful.

---

## 19. Collaboration between groups

Groups are encouraged to discuss general data-handling and machine-learning problems with each other.

Because several groups work within the same learning-analytics domain, useful discussions may include:

* understanding the Edge-LMS data structure,
* Python and data-handling techniques,
* visualization methods,
* machine learning concepts,
* evaluation methods,
* and debugging approaches.

However, each group must solve and document its own assigned project problem.

Sharing complete project solutions, project-specific code, results, or reports between groups is not acceptable.

---

## 20. What your project should demonstrate

A successful project should demonstrate that your group can move through the complete chain:

**information system → raw data → artificial data → prepared analytical data → machine learning → evaluation → interpretation**

The quality of the project is not determined only by the performance of the final model.

A simple model supported by careful data preparation, sound evaluation and thoughtful interpretation may demonstrate stronger learning than a complicated model used without understanding.
