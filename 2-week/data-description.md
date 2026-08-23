Yes. The code block was the problem. I’ll use normal formatted text from now on so you can copy the rendered document directly.

# Edge-LMS Data Guide

## 1. What is Edge-LMS data?

Edge-LMS is the course system used as the application context for our project work.

When people use an information system, the system produces and stores different kinds of data.

Examples include:

* users and groups
* activity events
* task submissions
* quiz attempts
* exam attempts
* grades
* calculated measures

In this course we use **synthetic data** that resembles Edge-LMS data.

The synthetic records do not represent real students.

---

## 2. Data does not start as one table

Edge-LMS is mainly a file-based application.

Its source data can appear as:

* JSON files
* JSONL files
* log files
* submitted files
* records stored in different directories

Different parts of the system can also use different record structures.

A typical workflow is:

**find → understand → load → validate → combine → prepare → analyse**

Do not assume that the data is already analysis-ready.

---

## 3. Source data and teaching data

You may encounter two kinds of examples.

### Source-like examples

These resemble how Edge-LMS itself stores information.

They help you investigate:

* file structures
* nested JSON
* different record types
* identifiers
* inconsistencies between sources

### Teaching dataset

For later analysis, data may be provided in a simplified structure such as:

* `students.jsonl`
* `groups.jsonl`
* `activity_daily.jsonl`
* `task_attempts.jsonl`
* `quiz_attempts.jsonl`
* `exam_attempts.jsonl`
* `grades.jsonl`
* `concept_measures.jsonl`

Not every exercise will use every file.

The teaching dataset is easier to analyse, but it represents the same kinds of information found in the source system.

---

## 4. What does one record represent?

Always determine the **record grain** before analysing data.

| Dataset            | One record may represent                   |
| ------------------ | ------------------------------------------ |
| `students`         | one student                                |
| `groups`           | one student-group membership               |
| `activity_daily`   | activity for one student during one period |
| `task_attempts`    | one task attempt                           |
| `quiz_attempts`    | one quiz attempt                           |
| `exam_attempts`    | one exam attempt                           |
| `grades`           | one grade observation                      |
| `concept_measures` | one calculated concept measurement         |

One student can therefore occur many times in some datasets.

This matters when datasets are joined and when statistics are calculated.

---

## 5. Identifiers connect datasets

The teaching data uses identifiers such as:

* `student_key`
* `course_key`
* `group_key`
* `task_key`
* `attempt_key`

For example, the same `student_key` may occur in several datasets.

This makes it possible to connect related records.

An identifier tells you **which entity the record belongs to**.

It is not normally a measurement.

---

## 6. Relationships

Suppose `students.jsonl` contains one row per student, while `quiz_attempts.jsonl` contains several attempts per student.

The relationship is then:

**one student → many quiz attempts**

Before joining datasets, ask:

1. What does one record represent in each dataset?
2. Which identifier connects them?
3. Is the relationship one-to-one, one-to-many, or many-to-many?
4. What will one row represent after the join?

A technically successful join is not automatically a correct join.

---

## 7. Raw, derived and inferred data

Not every value has the same origin.

### Raw or observed data

Recorded directly from an action or source.

Examples:

* task submitted
* quiz attempt
* score stored by the system
* activity timestamp

### Derived data

Calculated from other values.

Examples:

* number of attempts
* average score
* days since activity
* concept coverage

### Inferred data

A rule or model interprets other observations.

For example, a system might infer an activity status from several events.

An inferred value is **not the same thing as an observed fact**.

Always check where a variable came from before interpreting it.

---

## 8. Missing values

A missing value can have several meanings:

* no action occurred
* the feature was not enabled
* the field does not apply
* the source record is missing
* processing failed
* a relationship could not be resolved

**Missing does not automatically mean zero.**

Investigate the meaning before filling or removing missing values.

---

## 9. Data quality

When inspecting Edge-LMS-style data, look for:

* missing values
* unexpected values
* inconsistent categories
* incorrect technical types
* duplicate records
* unresolved identifiers
* different timestamp formats
* records with different structures

Do not immediately correct everything.

First ask:

**What does this value mean, and why might it look like this?**

---

## 10. Data safety

The original application can contain information that is not appropriate for ordinary student analysis.

The course dataset therefore excludes or replaces information such as:

* names
* email addresses
* real student numbers
* login IDs
* IP addresses
* password and session information
* security data
* teacher comments
* unnecessary free text
* sensitive risk classifications

Use only the provided course data.

Do not attempt to identify real people from synthetic or pseudonymous records.

---

## 11. Using the synthetic examples

Download the synthetic Edge-LMS example package provided with the course.

Start by exploring it rather than immediately writing analysis code.

For each example, determine:

1. What type of file is this?
2. What does one record represent?
3. What fields occur?
4. Which fields are identifiers?
5. Which fields are categorical, numerical, datetime, or text?
6. Which values are raw, derived, or inferred?
7. Could this record be connected to another dataset?
8. What data-quality problems might occur?
9. What information would you need from the data dictionary?

---

## 12. Typical workflow

When working with the project data:

**Project problem → identify relevant data → understand records and variables → identify relationships → load → validate → combine → prepare → analyse/model → validate results → interpret**

Do not start by choosing a machine-learning algorithm.

Start with the **problem and the data**.

---

## Key Ideas

* Edge-LMS data does not begin as one clean table.
* Always know what one record represents.
* Identifiers connect data but are not measurements.
* Different datasets may have different record grains.
* Missing values need interpretation.
* Derived and inferred values are different from directly observed data.
* Keep the project problem in mind when deciding which data is actually needed.
* **Understanding the data comes before machine learning.**
