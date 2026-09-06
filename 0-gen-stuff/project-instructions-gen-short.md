# Data Handling and Machine Learning – Group Project Instructions

## Purpose

The project practices a complete **data handling and machine learning workflow** using learning analytics data from Edge-LMS.

The goal is not only to train a model. You should understand how data is produced, prepared, analysed, modelled, evaluated and interpreted.

## Project topics

Each group receives a project topic randomly.

Before the announced deadline, groups may:

* exchange topics with another group, or
* return their topic and select an available alternative.

After the deadline, topics are fixed.

Each group receives a separate **Project Card** describing its problem.

## 1. Understand the raw data

Use Edge-LMS yourself and inspect the data created by your actions, such as:

* quiz attempts,
* scores,
* module progress,
* and activity events.

The purpose is to understand how user actions become raw data.

Your own activity data will not be large enough for machine learning.

## 2. Use the provided artificial data

The course provides a realistic artificial Edge-LMS dataset. You do not need to generate the complete dataset yourself.

Read its manifest, data dictionary and generation summary. Select the source files and variables needed for your project. If a simple student generator is available, you may optionally create a reproducible variant by choosing documented parameters and a random seed.

## 3. Prepare the analytical dataset

Transform the raw data into a dataset suitable for your project.

Depending on the project, one row might represent a:

* student,
* quiz attempt,
* question,
* module,
* or activity period.

This may require joining files, filtering, aggregation, handling missing values and creating features.

Be able to explain how the final dataset was produced.

## 4. Explore the data

Use suitable statistics and visualizations to understand:

* distributions,
* missing values,
* unusual observations,
* relationships between variables,
* and possible data-quality problems.

Include analyses that help answer your project question.

## 5. Define the machine learning task

Clearly define:

* what you are trying to learn or predict,
* the unit of observation,
* the features,
* the target, if applicable,
* and how success will be evaluated.

Choose methods that fit the problem. The Project Card does not prescribe a particular algorithm.

## 6. Build and compare models

Start with a simple baseline.

Then investigate a small number of suitable machine learning approaches.

Explain why you selected them and compare their results.

More complicated is not automatically better.

## 7. Evaluate and interpret

Use evaluation methods suitable for your problem.

Analyse:

* how well the method works,
* where it fails,
* which observations are difficult,
* and what the results mean for the original problem.

Where appropriate, investigate which features or patterns appear important.

Remember:

**Prediction does not prove causation.**

## 8. Compare with the known artificial-data process

Use the public generation summary and any variant parameters you selected.

Compare these with your results:

* Did the analysis discover the documented patterns?
* Did it miss important patterns?
* Did it appear to discover relationships that were not documented?

## 9. Consider limitations and responsible use

Discuss important limitations, such as:

* poor or missing data,
* class imbalance,
* information leakage,
* generalization to real data,
* privacy,
* fairness,
* and incorrect predictions.

Do not use identifiable classmates' behaviour as your project dataset.

## 10. Make the work reproducible

Organize your project so that another person can understand:

**provided synthetic source data → preprocessing → analytical dataset → model → evaluation**

Your processing must be repeatable. If you generate an optional variant, record its parameters and seed.

## Collaboration between groups

You may discuss general problems with other groups, including:

* Edge-LMS data structures,
* Python and data handling,
* visualizations,
* machine learning concepts,
* and debugging.

Each group must still produce its own project solution, code, analysis and results.

## What a good project demonstrates

A good project demonstrates that your group can move through the complete process:

**information system → synthetic source data → analytical dataset → machine learning → evaluation → interpretation**

The quality of the project is not determined only by the final model score.
