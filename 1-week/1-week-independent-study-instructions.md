# Week 1 Study Package

**Preparation for Monday 2: Understanding and Preparing Data**

Expected independent study time: **approximately 28 hours**

Suggested schedule: approximately **7 hours per day from Tuesday to Friday**.

This week follows the data workflow:

**source data → understand → retrieve → combine → validate → prepare → store → query**

You will work with **fully synthetic data** based on realistic Edge-LMS data structures. Synthetic data is used by default to avoid exposing real student records or unnecessary personal information.

---

# Tuesday – Understand Data and Data Storage

**Suggested time: ~7 h**

## 1. Understanding Data – ~2 h

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

## 2. Pandas Fundamentals – ~2.5 h

Study and run selected examples from Jake VanderPlas, *Python Data Science Handbook*:

* [Introducing Pandas Objects](https://jakevdp.github.io/PythonDataScienceHandbook/03.01-introducing-pandas-objects.html)
* [Data Indexing and Selection](https://jakevdp.github.io/PythonDataScienceHandbook/03.02-data-indexing-and-selection.html)
* [Operating on Data in Pandas](https://jakevdp.github.io/PythonDataScienceHandbook/03.03-operations-in-pandas.html)
* [Handling Missing Data](https://jakevdp.github.io/PythonDataScienceHandbook/03.04-missing-values.html)

Run selected examples yourself in Jupyter.

## 3. Getting, Storing and Retrieving Data – ~2 h

Study the course material:

**Getting, Storing and Retrieving Data: Files, JSON and Databases**

Focus on:

* data sources;
* structured, semi-structured and unstructured data;
* JSON, JSONL and CSV;
* files and directory structures;
* schemas and data dictionaries;
* identifiers and relationships;
* raw, derived and prepared data;
* databases and SQL;
* why different data-management solutions exist;
* volume, velocity and variety.

## 4. Additional reading – ~0.5 h

Browse:

* [Zaki & Meira – Chapter 1: Data Mining and Analysis](https://dataminingbook.info/book_html/chap1/book.html)
* [Chapter 2: Numeric Attributes](https://dataminingbook.info/book_html/chap2/book.html)
* [Chapter 3: Categorical Attributes](https://dataminingbook.info/book_html/chap3/book.html)

Concentrate on concepts rather than mathematical details.

---

# Wednesday – From Source Records to Usable Data

**Suggested time: ~7 h**

Edge-LMS does not originally store everything in one clean table. Its data can occur in JSON, JSONL, task files, logs and different directory structures. Different subsystems also use different identifiers and record structures.

## Exercise 1: Inspect Source-Like Data

You will receive a small collection of **synthetic source-like examples**.

Investigate:

1. What does one record represent?
2. Is the record JSON, JSONL or another form?
3. Which fields are identifiers?
4. Which fields contain categories, numbers, dates or text?
5. Are some fields nested?
6. Are all records structured identically?
7. Which values are raw observations?
8. Which values are calculated or inferred?
9. Which fields could connect this record with another dataset?
10. Which fields should not normally be included in a student analysis dataset?

Do not assume that a field is safe or useful simply because it exists in the source system.

## Exercise 2: Inspect the Teaching Export

The main course dataset follows a normalized structure similar to:

```text
course-data/
├── manifest.json
├── students.jsonl
├── groups.jsonl
├── attendance_sessions.jsonl
├── activity_daily.jsonl
├── task_attempts.jsonl
├── quiz_attempts.jsonl
├── exam_attempts.jsonl
├── grades.jsonl
├── concept_measures.jsonl
└── data_dictionary.md
```

The exact package used in the course may contain only the files needed for the exercise.

Using Python:

* find the available files;
* read JSONL records;
* load selected records into pandas DataFrames;
* inspect columns and values;
* compare the records with the data dictionary.

For each important variable, determine:

* technical representation;
* semantic meaning;
* missingness;
* whether it is stored, derived or inferred;
* what identifier connects it to other datasets.

The Edge-LMS data dictionary explicitly distinguishes these properties.

---

# Thursday – Combine, Prepare, Store and Query

**Suggested time: ~7 h**

## 1. Combine Related Data – ~2 h

Use selected JSONL files such as:

```text
students.jsonl
task_attempts.jsonl
quiz_attempts.jsonl
activity_daily.jsonl
```

Identify the appropriate keys and combine information where meaningful.

The teaching export uses normalized pseudonymous keys such as:

```text
student_key
course_key
task_key
attempt_key
group_key
```

Do not attempt to reconstruct original student identities.

Consider:

* What does one row represent?
* Is the relationship one-to-one or one-to-many?
* Could joining create duplicate rows?
* Is the key valid in both datasets?

The real source system contains several identifier conventions, which is one reason normalization is needed before analysis.

## 2. Inspect and Prepare the Data – ~2.5 h

Check:

* missing values;
* invalid values;
* unexpected categories;
* duplicates;
* data types;
* ranges;
* timestamps;
* unresolved relationships.

Do not automatically replace every missing value.

Missingness can have different meanings, for example:

* feature not enabled;
* no student action;
* source record missing;
* parser failure;
* field not applicable;
* join unresolved.

These should not automatically be treated as the same kind of missing value.

Create an analysis-ready DataFrame and document important changes:

> **What did you change? Why?**

Keep the original data unchanged.

## 3. Store and Retrieve with SQLite – ~1.5 h

Load selected prepared tables into SQLite.

Practise:

```sql
SELECT *
FROM students;
```

Filtering:

```sql
SELECT student_key, score
FROM quiz_attempts
WHERE score > 0.7;
```

Aggregation:

```sql
SELECT student_key, AVG(score)
FROM quiz_attempts
GROUP BY student_key;
```

and one simple join between related tables.

The purpose is not to learn SQL comprehensively.

The goal is to understand:

**data storage → relationships → retrieval → analysis**

## 4. Start Your Concept Map – ~1 h

Start your simplified concept map based on this week's theory.

Possible concepts include:

**Data Source – JSONL – Schema – Identifier – Relationship – Missing Data – Data Quality – Preprocessing – Database**

Select only the concepts that you consider important, difficult, interesting or strongly connected.

---

# Friday – Consolidate and Prepare for Monday

**Suggested time: ~7 h**

## 1. Complete Practical Work – ~3 h

Finish your notebook and prepared data.

Check that:

* your notebook runs from beginning to end;
* the original data remains unchanged;
* your transformations are reproducible;
* important preprocessing decisions are explained;
* joins use meaningful keys;
* prepared outputs can be recreated from the source data.

## 2. Complete the Concept Map – ~1 h

Finalize your simplified concept map.

Bring it to Monday's session.

## 3. Preparation Quiz / Task – ~1 h

Complete the Week 1 preparation quiz or equivalent task.

Topics may include:

* semantic and technical data types;
* discrete and continuous data;
* identifiers;
* JSON and JSONL;
* schemas and data dictionaries;
* raw, derived and prepared data;
* missingness;
* data quality;
* preprocessing;
* relationships and joins;
* databases and SQL;
* basic pandas operations.

## 4. Review and Technical Catch-up – ~2 h

Use the remaining time according to your needs:

* practise pandas;
* practise reading JSON/JSONL;
* repeat SQL queries;
* investigate data relationships;
* review unclear concepts;
* resolve Python, Jupyter or Git problems.

If you need additional Python practice:

[Introduction to Statistical Learning – Introduction to Python Lab](https://intro-stat-learning.github.io/ISLP/labs/Ch02-statlearn-lab.html)

---

# Important Data-Safety Rule

The course dataset is synthetic unless explicitly stated otherwise.

Do not attempt to identify real students or connect synthetic/pseudonymous records to real people.

Fields such as names, email addresses, login IDs, student numbers, IP addresses, passwords, session information, teacher comments, raw security information and sensitive algorithmic risk classifications are not part of ordinary student datasets.

---

# Ready for Monday 2

Before Monday, you should have:

* studied the assigned theory;
* inspected source-like data records;
* loaded and explored JSONL data;
* used a data dictionary;
* identified semantic data types;
* combined related datasets;
* investigated missingness and data quality;
* prepared analysis-ready data;
* stored and retrieved selected data using SQLite;
* prepared your simplified concept map;
* completed the preparation quiz/task;
* a functioning course environment.

You do **not** need to master everything before Monday.

Monday will be used for:

**clarification → deeper data-quality and preprocessing problems → discussion → guided practical work → project preparation**
