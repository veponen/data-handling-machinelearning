# Week 1 Study Package

**Preparation for Monday 2: Understanding and Preparing Data**

Expected independent study time: **approximately 28 hours**

The suggested schedule is about **7 hours per day from Tuesday to Friday**. You may arrange the hours differently, but complete the required work before Monday.

## Learning goals

Before Monday, you should be able to:

* explain why understanding data comes before modelling;
* recognize important data types and explain what they mean;
* identify operations that are meaningful for different types of data;
* inspect a dataset using Python and pandas;
* identify common data-quality problems;
* perform basic data cleaning and transformation;
* explain basic alternatives for storing and retrieving data;
* justify important preprocessing choices.

---

# Tuesday – Understand the data and learn the basic tools

**Suggested time: ~7 h**

## 1. Course material: Understanding Data

Study:

**Understanding Data: Types, Meaning and Valid Operations**

Main topics:

* technical vs semantic data types;
* nominal, ordinal, interval and ratio scales;
* discrete and continuous variables;
* identifiers;
* dates and time;
* text;
* missing values;
* valid and invalid operations;
* implications for preprocessing and machine learning.

Complete the short exercises included in the material.

**Suggested time: ~2 h**

## 2. Pandas fundamentals

Study and run examples from Jake VanderPlas, *Python Data Science Handbook*:

1. [Introducing Pandas Objects](https://jakevdp.github.io/PythonDataScienceHandbook/03.01-introducing-pandas-objects.html)
2. [Data Indexing and Selection](https://jakevdp.github.io/PythonDataScienceHandbook/03.02-data-indexing-and-selection.html)
3. [Operating on Data in Pandas](https://jakevdp.github.io/PythonDataScienceHandbook/03.03-operations-in-pandas.html)
4. [Handling Missing Data](https://jakevdp.github.io/PythonDataScienceHandbook/03.04-missing-values.html)

Do not only read the examples. Run selected examples yourself in Jupyter.

**Suggested time: ~3 h**

## 3. Course material: Getting, Storing and Retrieving Data

Study the provided course material:

**Getting, Storing and Retrieving Data**

Main topics:

* where data comes from;
* files, APIs and databases;
* CSV and JSON;
* tables, rows, columns and keys;
* storing and retrieving data;
* combining data sources;
* when files are sufficient;
* when a database or another data-management solution is useful;
* data provenance and basic privacy considerations.

**Suggested time: ~1.5 h**

## 4. Additional perspective

Read briefly:

* [Zaki & Meira: Chapter 1 – Data Mining and Analysis](https://dataminingbook.info/book_html/chap1/book.html)
* [Zaki & Meira: Chapter 2 – Numeric Attributes](https://dataminingbook.info/book_html/chap2/book.html)
* [Zaki & Meira: Chapter 3 – Categorical Attributes](https://dataminingbook.info/book_html/chap3/book.html)

Do **not** study the mathematical details. Browse these chapters to reinforce the distinction between different forms of data.

**Suggested time: ~0.5 h**

---

# Wednesday – Understand a real dataset

**Suggested time: ~7 h**

## Exercise: Understand the Dataset

Use the dataset provided for the course.

Create a Jupyter notebook and investigate the data.

### Tasks

1. Load the dataset.
2. Determine its number of rows and columns.
3. Inspect its technical data types.
4. Explain what the important variables actually represent.
5. Classify variables according to their meaning.
6. Identify identifiers and variables that only appear numerical.
7. Find missing values.
8. Find suspicious or impossible values.
9. Check for duplicates.
10. Look for inconsistent categories.
11. Calculate useful descriptive statistics.
12. Create a few useful visualizations.
13. Suggest questions that could reasonably be investigated using the data.
14. Identify information you would need before trusting the dataset.

Your notebook should show both:

**what you found → how you found it**

Do **not** build a machine-learning model yet.

### Useful references

Return to these sections when needed:

* [Data Indexing and Selection](https://jakevdp.github.io/PythonDataScienceHandbook/03.02-data-indexing-and-selection.html)
* [Handling Missing Data](https://jakevdp.github.io/PythonDataScienceHandbook/03.04-missing-values.html)
* [Aggregation and Grouping](https://jakevdp.github.io/PythonDataScienceHandbook/03.08-aggregation-and-grouping.html)

**Suggested time: ~7 h**

---

# Thursday – Prepare the data

**Suggested time: ~7 h**

## Exercise: Prepare the Dataset

Continue using the same dataset.

Keep the original dataset unchanged and create a prepared version.

### Tasks

Practise:

* selecting relevant rows and columns;
* correcting inappropriate data types;
* handling missing values;
* investigating or removing duplicates;
* correcting inconsistent categories;
* identifying and handling invalid values;
* creating simple derived variables;
* grouping and summarizing data;
* saving the prepared dataset.

For important changes, briefly record:

> **What did you change? Why?**

There may be more than one reasonable solution.

### Useful references

* [Operating on Data in Pandas](https://jakevdp.github.io/PythonDataScienceHandbook/03.03-operations-in-pandas.html)
* [Handling Missing Data](https://jakevdp.github.io/PythonDataScienceHandbook/03.04-missing-values.html)
* [Aggregation and Grouping](https://jakevdp.github.io/PythonDataScienceHandbook/03.08-aggregation-and-grouping.html)

**Dataset preparation: ~5.5 h**

## Start your concept map

Review the theory studied during the week and begin your simplified concept map.

Choose concepts that you found:

* important;
* interesting;
* difficult;
* surprising; or
* strongly connected.

Do not try to include everything.

**Concept-map work: ~1.5 h**

---

# Friday – Complete, review and prepare for Monday

**Suggested time: ~7 h**

## 1. Complete your work

Finish:

* data-understanding notebook;
* data-preparation work;
* simplified concept map.

Check that your notebook can be run from beginning to end.

**Suggested time: ~3 h**

## 2. Preparation quiz/task

Complete the Week 1 preparation quiz or equivalent task.

Topics include:

* data types and meaning;
* discrete and continuous data;
* identifiers;
* missing values;
* data quality;
* preprocessing;
* data sources;
* storage and retrieval;
* basic pandas operations.

**Suggested time: ~1 h**

## 3. Review and practise

Use the remaining time according to your needs.

Possible activities:

* repeat difficult pandas operations;
* improve your notebook;
* investigate the dataset further;
* practise visualizations;
* review unclear concepts;
* resolve remaining Python, Jupyter or Git problems.

If you need additional Python practice, use:

[Introduction to Statistical Learning – Introduction to Python Lab](https://intro-stat-learning.github.io/ISLP/labs/Ch02-statlearn-lab.html)

Useful parts include:

* basic Python commands;
* numerical Python;
* indexing;
* loading data;
* selecting rows and columns;
* basic graphical and numerical summaries.

**Suggested time: ~3 h**

---

# Ready for Monday 2

Before Monday, you should have:

* studied the required theory;
* completed the data-understanding exercise;
* completed the data-preparation exercise;
* prepared your simplified concept map;
* completed the preparation quiz/task;
* a functioning course environment.

You do **not** need to master everything before Monday.

You should arrive already familiar with the basic concepts so that Monday can be used for:

**clarification → deeper exercises → problem solving → discussion → guided practical work**
