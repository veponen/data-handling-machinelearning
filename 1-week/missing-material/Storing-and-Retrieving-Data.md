# Getting, Storing and Retrieving Data: Files, JSON and Databases

Data analysis does not usually start with a perfect table.

Data may come from:

* application files;
* databases;
* APIs;
* forms;
* sensors;
* logs;
* documents;
* external datasets;
* generated or synthetic data.

Before analysing data, we need to understand:

> **Where does the data come from, how is it stored, how do different records relate to each other, and how can we retrieve the information we need?**

---

# 1. From a data source to analysis

A useful general workflow is:

**source data → retrieve → understand → validate → combine → prepare → analyse**

For example, a learning system may store:

* student records;
* quiz attempts;
* task submissions;
* activity records;
* grades.

These may exist in different files and structures.

Before asking:

> Which machine-learning algorithm should I use?

we first need to ask:

> Where is the required information?

and:

> How can these records be combined correctly?

---

# 2. Data can have different structures

## Structured data

Structured data follows a regular predefined structure.

For example:

| student_key | attempts | score |
| ----------- | -------: | ----: |
| STU_A       |        2 |  0.75 |
| STU_B       |        1 |  0.90 |

Rows represent observations and columns represent variables.

A relational database table is a common example of structured data.

---

## Semi-structured data

Semi-structured data has structure, but it does not have to be a simple rectangular table.

JSON is a common example:

```json
{
  "student_key": "STU_A",
  "quiz": {
    "attempt": 2,
    "score": 0.75
  }
}
```

The fields have names, but values can contain nested objects and lists.

Python includes built-in support for encoding and decoding JSON.

---

## Unstructured data

Some data does not naturally consist of predefined fields and columns.

Examples include:

* free text;
* images;
* audio;
* documents.

Even these files usually have some surrounding structure, such as:

* filename;
* timestamp;
* owner;
* file type;
* directory.

Later in this course, text will become especially important when we study natural-language processing.

---

# 3. Common file formats

## CSV

CSV is useful for rectangular tabular data.

Example:

```text
student_key,attempts,score
STU_A,2,0.75
STU_B,1,0.90
```

Advantages:

* simple;
* human-readable;
* widely supported;
* easy to load into pandas.

Limitations:

* weak support for nested structures;
* data types are not strongly represented;
* relationships between several datasets must be documented separately.

CSV is often excellent for an **analysis-ready table**.

---

# 4. JSON

JSON stores values using objects, arrays and basic value types.

Example:

```json
{
  "student_key": "STU_A",
  "active": true,
  "courses": ["COURSE_A", "COURSE_B"]
}
```

JSON is particularly useful when:

* records contain nested structures;
* different records may contain different fields;
* applications exchange structured information;
* data is naturally represented as objects rather than rows.

A JSON file can contain one object, a list of objects, or a more complex nested structure.

Pandas can read JSON data, and `json_normalize()` can transform nested semi-structured records into flatter tabular structures.

---

# 5. JSON Lines / JSONL

In this course you will also encounter **JSON Lines**, usually stored with the extension:

```text
.jsonl
```

In a JSONL file, **each line is one complete JSON value**.

Example:

```json
{"student_key":"STU_A","attempts":2,"score":0.75}
{"student_key":"STU_B","attempts":1,"score":0.90}
{"student_key":"STU_C","attempts":3,"score":0.82}
```

This is different from a normal JSON array:

```json
[
  {"student_key":"STU_A","attempts":2,"score":0.75},
  {"student_key":"STU_B","attempts":1,"score":0.90}
]
```

JSONL is useful when:

* data consists of many records;
* records are naturally processed one at a time;
* new records may be appended;
* files may become large;
* logs or event streams are stored.

Pandas can read line-delimited JSON directly.

---

# 6. One dataset may consist of several files

A course dataset might look like:

```text
course-data/
├── students.jsonl
├── groups.jsonl
├── activity_daily.jsonl
├── task_attempts.jsonl
├── quiz_attempts.jsonl
├── grades.jsonl
└── data_dictionary.md
```

This is similar to the synthetic teaching-data structure used in this course.

Each file answers a different question.

For example:

**students.jsonl**

> Who or what are the entities being studied?

**quiz_attempts.jsonl**

> What quiz attempts occurred?

**task_attempts.jsonl**

> What task attempts occurred?

**activity_daily.jsonl**

> What activity was observed during a period?

No single file necessarily contains everything needed for an analysis.

---

# 7. What does one row represent?

This question is extremely important.

Suppose:

```text
students.jsonl
```

contains **one row per student**.

But:

```text
quiz_attempts.jsonl
```

contains **one row per quiz attempt**.

One student may therefore occur once in one dataset and many times in another.

Example:

### Students

| student_key |
| ----------- |
| STU_A       |
| STU_B       |

### Quiz attempts

| student_key | attempt | score |
| ----------- | ------: | ----: |
| STU_A       |       1 |  0.55 |
| STU_A       |       2 |  0.75 |
| STU_B       |       1 |  0.90 |

This is a **one-to-many relationship**.

Before combining datasets, always ask:

> **What does one record represent?**

---

# 8. Identifiers connect data

Different datasets need common identifiers.

For example:

```text
student_key = STU_A
```

could appear in:

```text
students.jsonl
quiz_attempts.jsonl
task_attempts.jsonl
activity_daily.jsonl
```

The identifier allows records to be connected.

The teaching dataset uses pseudonymous identifiers such as:

* `student_key`
* `course_key`
* `task_key`
* `attempt_key`
* `group_key`

rather than operational student identifiers.

An identifier is not normally a numerical measurement.

For example:

```text
student_key = STU_123
```

tells us **which entity** a record belongs to.

It does not tell us how large, good or important that student is.

---

# 9. Be careful when joining datasets

Consider:

### students

| student_key | group |
| ----------- | ----- |
| STU_A       | G1    |
| STU_B       | G1    |

### attempts

| student_key | score |
| ----------- | ----: |
| STU_A       |  0.55 |
| STU_A       |  0.75 |
| STU_B       |  0.90 |

Joining them creates:

| student_key | group | score |
| ----------- | ----- | ----: |
| STU_A       | G1    |  0.55 |
| STU_A       | G1    |  0.75 |
| STU_B       | G1    |  0.90 |

This may be correct because the analysis is now at the **attempt level**.

But if you expected one row per student, something has changed.

Therefore ask before every join:

1. What does one row represent in dataset A?
2. What does one row represent in dataset B?
3. Which key connects them?
4. Is the relationship one-to-one, one-to-many or many-to-many?
5. What will one row represent after the join?

The original Edge-LMS implementation uses several different identifier conventions, which is one reason the teaching export normalizes identifiers before students analyse the data.

---

# 10. Schema

A **schema** describes the structure of data.

It may define things such as:

* field names;
* data types;
* required fields;
* relationships;
* allowed values.

For example:

```text
student_key    string, required
attempt        integer, required
score          number, 0–1
submitted_at   datetime
```

A schema answers:

> **How is this data structured?**

---

# 11. Data dictionary

A **data dictionary** explains what the fields mean.

For example:

| Field          | Meaning                         | Semantic type        |
| -------------- | ------------------------------- | -------------------- |
| `student_key`  | pseudonymous learner identifier | identifier           |
| `attempt`      | attempt sequence                | discrete numerical   |
| `score`        | normalized score                | continuous numerical |
| `submitted_at` | submission time                 | datetime             |

A data dictionary may also describe:

* allowed values;
* units;
* missing values;
* origin;
* whether a value is stored or calculated;
* relationships to other datasets;
* privacy considerations.

The course teaching data is accompanied by a data dictionary because field names alone are not sufficient for understanding the data. The Edge-LMS source analysis also distinguishes raw, calculated and inferred fields.

---

# 12. Raw, prepared and derived data

It is useful to keep different stages of data separate.

## Raw data

Data close to the original source.

```text
raw/
```

Avoid modifying it.

---

## Prepared data

Data that has been:

* cleaned;
* transformed;
* combined;
* validated;
* converted to appropriate types.

```text
prepared/
```

---

## Derived data

Values calculated from other data.

For example:

```text
days_since_activity
average_quiz_score
submission_count
```

These values did not exist directly in the original source records.

A good workflow is:

```text
raw data
   ↓
validation
   ↓
prepared data
   ↓
derived variables
   ↓
analysis / machine learning
```

> **Keep the raw data unchanged whenever possible.**

This allows preprocessing to be reproduced or corrected later.

---

# 13. Missing data requires explanation

A missing value does not always mean the same thing.

For example, a value might be missing because:

* the student performed no action;
* the feature was not enabled;
* the record was unavailable;
* a parser failed;
* a join could not be resolved;
* the value is genuinely not applicable.

The Edge-LMS data study specifically warns that these cases should not automatically be converted into one generic meaning such as zero.

For example:

```text
quiz_attempts = 0
```

and:

```text
quiz_attempts = unknown
```

are not necessarily the same thing.

---

# 14. Why use a database?

Files are often sufficient.

For example:

```text
students.jsonl
```

may be perfectly suitable for storing a small set of student records.

But imagine that you frequently need to ask:

> Which students belong to group G1?

> Which quiz attempts belong to those students?

> What is each student's average score?

> Which students submitted task A but not task B?

When data consists of several related collections, a database can make storage and retrieval easier.

---

# 15. Relational databases

A relational database organizes data into related tables.

For example:

### STUDENT

| student_key | group |
| ----------- | ----- |
| STU_A       | G1    |
| STU_B       | G1    |

### QUIZ_ATTEMPT

| attempt_key | student_key | score |
| ----------- | ----------- | ----: |
| A001        | STU_A       |  0.55 |
| A002        | STU_A       |  0.75 |
| A003        | STU_B       |  0.90 |

The field:

```text
student_key
```

connects the tables.

This avoids repeating all student information in every quiz-attempt record.

---

# 16. SQLite

For this course we can use **SQLite** for introductory database work.

SQLite is convenient because Python can access an SQLite database through its standard `sqlite3` module, without requiring students to operate a separate database server.

An SQLite database can be stored as a file such as:

```text
course-data.db
```

Inside that file we can have tables such as:

```text
students
quiz_attempts
task_attempts
```

---

# 17. Retrieving data with SQL

SQL is a language for working with relational databases.

You only need a few operations initially.

## Select rows

```sql
SELECT *
FROM students;
```

`SELECT` queries a database and returns rows of data.

---

## Select specific columns

```sql
SELECT student_key, score
FROM quiz_attempts;
```

---

## Filter

```sql
SELECT student_key, score
FROM quiz_attempts
WHERE score > 0.7;
```

---

## Aggregate

```sql
SELECT student_key, AVG(score)
FROM quiz_attempts
GROUP BY student_key;
```

---

## Join related tables

```sql
SELECT
    students.student_key,
    students.group_key,
    quiz_attempts.score
FROM students
JOIN quiz_attempts
    ON students.student_key = quiz_attempts.student_key;
```

The purpose of the Week 1 SQL work is **not to master SQL**.

It is to understand:

> **How can information be stored in related structures and retrieved when needed?**

---

# 18. Pandas and databases can work together

Files, databases and pandas are not competing alternatives.

A typical workflow might be:

```text
JSONL
   ↓
pandas DataFrame
   ↓
clean / transform
   ↓
SQLite
   ↓
SQL query
   ↓
pandas DataFrame
   ↓
analysis
```

Pandas can write DataFrame records into SQL tables using `DataFrame.to_sql()`, including through an SQLite connection, and can read SQL queries or tables back into DataFrames.

So we can choose the representation that is useful for each stage.

---

# 19. Which storage solution should you use?

There is no universally best solution.

| Situation                           | Possible solution   |
| ----------------------------------- | ------------------- |
| Small rectangular dataset           | CSV                 |
| Application record                  | JSON                |
| Many independent structured records | JSONL               |
| Nested data                         | JSON                |
| Several related entities            | relational database |
| Repeated structured queries         | database            |
| Analysis in Python                  | pandas DataFrame    |
| Exchange between systems            | JSON/CSV/API        |

The choice depends on:

* structure;
* amount of data;
* relationships;
* how data is produced;
* how it must be retrieved;
* how often it changes;
* what analysis will be performed.

Files and databases are alternative and complementary data-management solutions. In this course, file-based data handling is essential because the project source system uses files. Database work will be adjusted according to the group's previous SQL experience.

---

# 20. Connection to Big Data

Having several JSON files does **not automatically mean that we have Big Data**.

NIST describes Big Data in terms of extensive datasets characterized particularly by dimensions such as:

* **volume** – amount of data;
* **velocity** – speed at which data is generated or processed;
* **variety** – different forms and structures;
* **variability** – changes or inconsistencies,

where scalable architectures are required for efficient storage, manipulation and analysis.

Our course data gives us a small-scale example of some of the same problems:

```text
many users
× many actions
× several record types
× repeated events
× different structures
```

With 40 students this is not a Big Data problem.

But now imagine:

```text
40 students
```

becoming:

```text
4,000,000 users
```

and records arriving continuously.

The fundamental questions remain similar, but the required storage and processing architecture changes.

---

# 21. Data minimization and safety

A source system may contain much more information than an analysis requires.

For example, the actual Edge-LMS implementation can contain identity information, exact timestamps, security information, student work, assessment responses and derived behavioural measures.

That does **not** mean all of it should be copied into an analysis dataset.

The course uses synthetic data by default.

Ordinary student datasets should not contain information such as:

* names;
* email addresses;
* real student numbers;
* login IDs;
* IP addresses;
* password or session information;
* security logs;
* unreviewed student free text;
* teacher comments;
* sensitive risk classifications.

The Edge-LMS teaching-data design deliberately replaces operational identities with package-local pseudonymous keys and minimizes unnecessary fields.

A useful principle is:

> **Use the data needed for the stated purpose—not every field that happens to exist.**

---

# 22. A practical data-management workflow

When you receive a new collection of data:

### 1. Inspect the files

What formats are present?

### 2. Determine the record grain

What does one record represent?

### 3. Read the documentation

What do the fields mean?

### 4. Identify keys

How can datasets be connected?

### 5. Preserve the source

Do not overwrite raw data.

### 6. Validate

Check structure, types, missing values and ranges.

### 7. Combine where justified

Use meaningful keys and understand the resulting row structure.

### 8. Prepare

Create analysis-ready variables and tables.

### 9. Store appropriately

Files may be sufficient, or a database may be useful.

### 10. Retrieve only what you need

Use Python, pandas or SQL according to the task.

---

# Short Exercises

## Exercise 1 – Choose a representation

Suggest a suitable representation and explain your choice:

1. One table containing 100 measurements.
2. Thousands of application events produced continuously.
3. A customer record containing several addresses and phone numbers.
4. Students, courses and enrollments that must be queried repeatedly.
5. A prepared table to be opened in spreadsheet software.

Possible alternatives include:

**CSV – JSON – JSONL – relational database**

There may be more than one reasonable answer.

---

## Exercise 2 – What does one record represent?

Consider:

```json
{"student_key":"STU_A","quiz_key":"Q1","score":0.60}
{"student_key":"STU_A","quiz_key":"Q2","score":0.80}
{"student_key":"STU_B","quiz_key":"Q1","score":0.75}
```

Answer:

1. What does one row represent?
2. How many students are represented?
3. How many quiz-result records are represented?
4. Which field connects these records to a student table?

---

## Exercise 3 – Identify raw and derived data

Suppose the source contains:

```text
student_key
quiz_score
submitted_at
```

An analysis later calculates:

```text
average_score
days_since_submission
number_of_attempts
```

Which variables are source values and which are derived?

Why should the distinction be documented?

---

## Exercise 4 – Join carefully

Dataset A contains one row per student.

Dataset B contains five task attempts for the same student.

What happens to that student's row when A and B are joined?

Why might this matter when calculating statistics?

---

## Exercise 5 – Files or database?

You have:

```text
students.jsonl
tasks.jsonl
quiz_attempts.jsonl
grades.jsonl
```

You repeatedly need to find:

> all quiz attempts and task grades belonging to students in a particular group.

Would you continue using the files directly, transform them into analysis tables, load them into a database, or use some combination?

Explain your decision.

---

# Key Ideas

Remember these principles:

> **Data does not necessarily arrive as one table.**

> **Always know what one record represents.**

> **Identifiers connect data but are not measurements.**

> **A schema describes structure; a data dictionary explains meaning.**

> **Keep raw data separate from prepared and derived data.**

> **Files and databases solve different data-management problems.**

> **Only retrieve and expose data that is appropriate for the purpose.**

> **Understanding storage and relationships is part of understanding the data.**
