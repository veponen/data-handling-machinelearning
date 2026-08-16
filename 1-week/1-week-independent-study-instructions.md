# Week 1 Study Package

**Preparation for Monday 2: Understanding and Preparing Data**

Expected independent study time: **approximately 28 hours**

The suggested schedule is approximately **7 hours per day from Tuesday to Friday**.

The main idea of the week is:

**find data → understand its structure and meaning → retrieve it → combine it → inspect quality → prepare it for analysis**

You will work with both tabular data and project-style JSON data.

---

# Tuesday – Understand Data and Data Storage

**Suggested time: ~7 h**

## 1. Understanding Data

Study the course material:

**Understanding Data: Types, Meaning and Valid Operations**

Focus on:

* technical vs semantic data types;
* nominal, ordinal, interval and ratio data;
* discrete and continuous variables;
* identifiers;
* datetime and text;
* missing values;
* valid and invalid operations;
* implications for preprocessing and machine learning.

Complete the short exercises included in the material.

**Suggested time: ~2 h**

## 2. Pandas Fundamentals

Study and run selected examples from Jake VanderPlas, *Python Data Science Handbook*:

* [Introducing Pandas Objects](https://jakevdp.github.io/PythonDataScienceHandbook/03.01-introducing-pandas-objects.html)
* [Data Indexing and Selection](https://jakevdp.github.io/PythonDataScienceHandbook/03.02-data-indexing-and-selection.html)
* [Operating on Data in Pandas](https://jakevdp.github.io/PythonDataScienceHandbook/03.03-operations-in-pandas.html)
* [Handling Missing Data](https://jakevdp.github.io/PythonDataScienceHandbook/03.04-missing-values.html)

Run examples yourself in Jupyter. Do not only read them.

**Suggested time: ~2.5 h**

## 3. Getting, Storing and Retrieving Data

Study the course material:

**Getting, Storing and Retrieving Data: Files, JSON and Databases**

Focus on:

* where data comes from;
* structured, semi-structured and unstructured data;
* CSV and JSON;
* files and directory structures;
* schemas and data dictionaries;
* raw vs prepared data;
* retrieving and combining records;
* basic relational databases;
* why different data-management solutions are needed;
* volume, velocity and variety.

**Suggested time: ~2 h**

## 4. Short additional reading

Browse the introductory sections of:

* [Zaki & Meira – Chapter 1: Data Mining and Analysis](https://dataminingbook.info/book_html/chap1/book.html)
* [Chapter 2: Numeric Attributes](https://dataminingbook.info/book_html/chap2/book.html)
* [Chapter 3: Categorical Attributes](https://dataminingbook.info/book_html/chap3/book.html)

Concentrate on the concepts. Mathematical details are not required yet.

**Suggested time: ~0.5 h**

---

# Wednesday – Explore Project-Style Data

**Suggested time: ~7 h**

## Exercise: From Files to Data

You will receive a directory containing several artificial JSON files representing records from an information system.

A simplified structure may look like:

```text
raw/
├── students/
│   ├── SYN001.json
│   ├── SYN002.json
│   └── ...
├── activity/
├── quiz_attempts/
└── task_submissions/
```

The final structure will follow the course dataset documentation.

## Part A – Understand the files

Investigate:

1. How many files are present?
2. What does one file represent?
3. What fields occur in each type of record?
4. Which fields are identifiers?
5. Which fields can connect records from different sources?
6. Are all records structured in the same way?
7. Are some values missing?
8. Are there nested structures?
9. Which fields contain numbers, categories, dates or text?
10. What information would you need from a data dictionary before interpreting the fields?

## Part B – Retrieve and combine

Using Python:

* find files programmatically;
* load JSON records;
* inspect nested structures;
* combine several records;
* create one or more pandas DataFrames;
* retain identifiers needed to connect datasets.

For example:

```python
from pathlib import Path
import json

files = Path("raw/students").glob("*.json")
```

Use `pandas.json_normalize()` where nested records need to be transformed into tabular form.

## Part C – Inspect the resulting data

Determine:

* number of observations;
* number of variables;
* technical data types;
* semantic data types;
* missing values;
* suspicious values;
* duplicate observations;
* inconsistent categories.

Create a few useful summaries and visualizations.

**Do not build a machine-learning model yet.**

---

# Thursday – Prepare, Store and Retrieve Data

**Suggested time: ~7 h**

Continue with Wednesday's data.

## 1. Prepare the Data – ~4 h

Create an analysis-ready version while keeping the original raw data unchanged.

Practise:

* selecting useful fields;
* correcting data types;
* handling missing values;
* correcting inconsistent categories;
* investigating invalid values;
* removing or resolving duplicates;
* deriving useful variables;
* combining information from different files;
* grouping and summarizing observations.

For important changes, record briefly:

> **What did you change? Why?**

Save prepared results separately from the raw data.

For example:

```text
prepared/
├── students.csv
├── quiz_attempts.csv
└── activity.csv
```

## 2. Basic Database Exercise – ~1.5 h

Create or use a small **SQLite database** containing selected prepared data.

Practise at least:

```sql
SELECT *
FROM students;
```

a filtered query:

```sql
SELECT student_id, score
FROM quiz_attempts
WHERE score > 0.7;
```

and an aggregation such as:

```sql
SELECT student_id, AVG(score)
FROM quiz_attempts
GROUP BY student_id;
```

The purpose is not to learn SQL comprehensively.

The goal is to understand the difference between:

**storing records → retrieving selected information → loading data for analysis**

## 3. Start Your Concept Map – ~1.5 h

Review the week's theory.

Prepare a simplified concept map containing concepts that you found:

* important;
* interesting;
* difficult;
* surprising; or
* strongly connected.

Possible concepts could come from areas such as:

**Data Source – JSON – Schema – Identifier – Data Type – Data Quality – Database – Preprocessing**

Do not try to include everything.

---

# Friday – Consolidate and Prepare for Monday

**Suggested time: ~7 h**

## 1. Finish Practical Work – ~3 h

Complete your notebooks and prepared data.

Check that:

* the notebook can run from beginning to end;
* raw data has not been overwritten;
* important preprocessing choices are explained;
* relationships between datasets are understandable;
* prepared outputs can be reproduced from the raw data.

## 2. Complete the Concept Map – ~1 h

Finalize your simplified concept map.

Bring it to Monday's session.

## 3. Preparation Quiz / Task – ~1 h

Complete the preparation quiz or equivalent task.

Topics may include:

* semantic and technical data types;
* discrete and continuous data;
* identifiers;
* missing values;
* JSON and CSV;
* schemas and data dictionaries;
* raw and prepared data;
* data quality;
* preprocessing;
* databases and retrieval;
* basic pandas operations.

## 4. Review and Technical Catch-up – ~2 h

Use the remaining time according to your needs:

* practise pandas;
* practise loading JSON;
* repeat SQL queries;
* improve visualizations;
* resolve Python, Jupyter or Git problems;
* review unclear concepts.

If you need additional Python practice:

[Introduction to Statistical Learning – Introduction to Python Lab](https://intro-stat-learning.github.io/ISLP/labs/Ch02-statlearn-lab.html)

---

# Ready for Monday 2

Before Monday, you should have:

* studied the assigned theory;
* worked with several data files;
* loaded and combined JSON data;
* inspected data types and data quality;
* prepared analysis-ready data;
* practised basic storage and retrieval using SQLite;
* prepared your simplified concept map;
* completed the preparation quiz/task;
* a functioning course environment.

You do **not** need to master everything before Monday.

Monday will be used for:

**clarification → deeper data-quality and preprocessing problems → discussion → guided practical work → project preparation**
