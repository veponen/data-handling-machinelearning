# Edge-LMS Project Data – Student Guide

## 1. Purpose of This Guide

This course uses **synthetic data based on the Edge-LMS data model**.

The purpose is to work with realistic:

* file structures;
* JSON and JSONL records;
* identifiers and relationships;
* repeated observations;
* missing data;
* derived variables;
* data-quality problems;

without exposing real student records.

The real Edge-LMS system stores data mainly in **files and directories**, rather than in one relational database. Relevant formats include JSON, JSONL, logs, submitted files, and derived analysis records. 

A central project task is therefore to learn how to move from:

**source files → usable data → analysis table → machine-learning pipeline**

---

# 2. What Data Exists in Edge-LMS?

Edge-LMS can produce several different types of student-related data.

Not all of this data is suitable for student projects.

| Data area                    | Examples                                                    | Normal project use      |
| ---------------------------- | ----------------------------------------------------------- | ----------------------- |
| Student/account data         | activation, course membership, class information            | synthetic and minimized |
| Groups                       | group membership                                            | yes, synthetic          |
| Activity                     | login/logout events, latest activity, activity counts       | selected and aggregated |
| Task submissions             | attempts, submission times, file type, selected metrics     | yes, selected fields    |
| Process-of-work data         | editing duration, keystrokes, paste counts, length changes  | normally excluded       |
| Quizzes                      | attempts, scores, timing                                    | yes, selected fields    |
| Exams                        | attempts, scores, timing                                    | restricted / selected   |
| Grades                       | scores, attempt counts, grading information                 | selected                |
| Attendance                   | recorded attendance sessions                                | selected                |
| Concept maps                 | concepts, relations, coverage measures                      | selected                |
| Text analysis                | word counts, structure, readability and related measures    | selected / synthetic    |
| Announcements and feedback   | read, acknowledgement and feedback-view information         | normally not needed     |
| Risk and similarity analysis | similarity scores, risk/watch classifications               | normally excluded       |
| Identity and security data   | names, email, IP addresses, passwords, sessions, audit data | never included          |

The complete operational system contains considerably more information than an ordinary teaching dataset.  

---

# 3. Where Is the Data in the Downloadable Examples?

The downloadable example package contains **synthetic source-like Edge-LMS files**.

These examples show how different kinds of information may exist before they are transformed into an analysis-ready dataset.

| Data area                | Example file                       | What it represents                            |
| ------------------------ | ---------------------------------- | --------------------------------------------- |
| Students/accounts        | `users.json`                       | current account records                       |
| Groups                   | `groups.json`                      | current groups and members                    |
| Latest activity          | `last_seen-SYN001.json`            | latest observed authenticated activity        |
| Activity and quiz events | `activity-SYN001.jsonl`            | a sequence of activity/log records            |
| Task submission          | `submission-SYN001.txt`            | one submitted text artifact                   |
| Process of work          | `pow-SYN001.json`                  | measurements associated with one task attempt |
| Concept measures         | `concept-measure-SYN001.json`      | derived concept-related measurements          |
| Grade V1                 | `grade-v1-SYN001.json`             | aggregate grading information                 |
| Grade V2                 | `grade-v2-SYN001.json`             | attempt-level grading information             |
| Structure measures       | `structure-metrics.jsonl`          | derived document-structure records            |
| Quiz session             | `quiz-session-SYN001.json`         | one quiz runtime/session record               |
| Exam session             | `exam-session-SYN002.json`         | one exam session                              |
| Exam results             | `exam-results-SYN002.jsonl`        | submitted exam-result records                 |
| Attendance sessions      | `attendance-sessions.json`         | available attendance sessions                 |
| Attendance detail        | `attendance-session-DEMO-W01.json` | recorded attendees for one session            |
| Announcement             | `announcement-SYN001.json`         | one student-targeted announcement             |

The files deliberately have different structures.

Some contain:

* one JSON object;
* arrays of objects;
* one JSON object per line;
* text artifacts;
* derived measurements.

This heterogeneity is part of the data-processing problem.

---

# 4. Source Data Is Not an ML Dataset

The downloadable files are **not already a machine-learning table**.

For example:

```text
users.json
activity-SYN001.jsonl
grade-v1-SYN001.json
concept-measure-SYN001.json
```

may all contain information relevant to one project.

A typical pipeline is:

```text
Edge-LMS source files
        ↓
Read JSON / JSONL / files
        ↓
Understand records and variables
        ↓
Select relevant fields
        ↓
Identify relationships
        ↓
Validate and clean
        ↓
Combine records
        ↓
Create derived variables
        ↓
Construct analysis table
        ↓
Machine-learning pipeline
```

The final table depends on the **project question**.

There is no single analysis table that is correct for every project.

---

# 5. Proposed Analysis-Oriented Data

For teaching and analysis, Edge-LMS source information can be normalized into datasets such as:

```text
course-data/
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

These names describe a **proposed normalized teaching export**. They are not the names of the original operational Edge-LMS source files. 

The distinction is important:

> **source files describe how the application stores data; analysis datasets describe how we organize data for a particular analytical purpose.**

---

# 6. Students

## Source example

```text
users.json
```

The real account store can contain information such as:

* account ID;
* student number;
* name;
* email;
* role;
* course memberships;
* group memberships;
* activation state;
* account timestamps;
* credential-related information. 

Most of these fields should **not** enter student analysis.

## Analysis representation

A normalized:

```text
students.jsonl
```

might contain only:

* `student_key`;
* course membership;
* activation state where needed;
* safe broad cohort information.

Names, email addresses, operational login IDs and student numbers are excluded. 

---

# 7. Groups

## Source example

```text
groups.json
```

A group record contains information about:

* course;
* group;
* members.

The operational group member identifier is not necessarily the same identifier used by all other Edge-LMS datasets. 

## Analysis representation

A normalized group record may contain:

```text
student_key
group_key
course_key
```

One student can belong to a group, and one group normally contains several students.

---

# 8. Activity

## Source examples

```text
last_seen-SYN001.json
activity-SYN001.jsonl
```

`last_seen` represents the latest observed authenticated request.

Activity logs contain selected system events, for example:

* login;
* logout;
* quiz-related actions.

The activity log is **not a complete page-view or clickstream history**. 

Therefore:

> Absence of an activity event does not necessarily mean absence of all learning activity.

## Possible analysis variables

Source records could be transformed into variables such as:

```text
activity_count_week
days_since_activity
quiz_activity_count
submission_activity_count
```

These are **derived variables**.

---

# 9. Task Submissions

## Source example

```text
submission-SYN001.txt
```

Operational Edge-LMS task submissions are primarily stored as files inside directory structures containing information about:

* course;
* module;
* submodule;
* task type;
* student;
* submission time. 

The submitted file itself may contain sensitive student work.

## Possible analysis representation

A normalized:

```text
task_attempts.jsonl
```

could contain selected information such as:

* `student_key`;
* `task_key`;
* `attempt_key`;
* attempt sequence;
* coarse submission time;
* artifact type;
* artifact-size category;
* selected approved measures. 

---

# 10. Process-of-Work Data

## Source example

```text
pow-SYN001.json
```

For some enabled tasks, Edge-LMS can measure:

* keystroke count;
* paste count;
* active seconds;
* editing duration;
* text-length changes;
* file size;
* whether the artifact changed.

These measurements need careful interpretation.

For example:

> `active_seconds` is not the same thing as time spent learning.

> Paste count does not prove authorship or misconduct.

These variables are normally excluded from ordinary student projects. 

They may be useful in a specifically designed exercise about **measurement error, interpretation, ethics or fairness**.

---

# 11. Quiz Data

## Source examples

```text
quiz-session-SYN001.json
activity-SYN001.jsonl
```

Quiz information can include:

* student;
* course/module/submodule;
* questions;
* answers;
* scores;
* start/end times;
* attempts.

The source logs can contain several records associated with one logical quiz attempt. A raw line count must therefore not automatically be interpreted as the number of quiz attempts. 

## Analysis representation

A normalized:

```text
quiz_attempts.jsonl
```

might contain one row per logical attempt:

```text
student_key
quiz_key
attempt_sequence
score
max_score
duration
```

Live questions and answers should normally be excluded from general project data.

---

# 12. Exam Data

## Source examples

```text
exam-session-SYN002.json
exam-results-SYN002.jsonl
```

Exam data can contain:

* student;
* exam;
* question set;
* answers;
* scores;
* start time;
* submission time;
* lateness;
* auto-submission status. 

Questions and answers are sensitive assessment data.

## Analysis representation

A normalized:

```text
exam_attempts.jsonl
```

might instead contain selected variables such as:

* student key;
* exam key;
* score or score band;
* lateness category;
* auto-submit status.

---

# 13. Grades

## Source examples

```text
grade-v1-SYN001.json
grade-v2-SYN001.json
```

Edge-LMS contains two relevant grading structures.

### Grade V1

This can aggregate information across attempts for a student/task.

### Grade V2

This is more attempt-oriented.

Grade records can contain:

* attempt information;
* scores;
* penalties;
* automated measures;
* grading provenance;
* feedback information. 

## Analysis caution

Grades are often **outcome variables**.

If a project predicts a later score, information calculated after that score was known must not be included as an input feature.

Otherwise the model suffers from **data leakage**. 

---

# 14. Attendance

## Source examples

```text
attendance-sessions.json
attendance-session-DEMO-W01.json
```

The attendance files contain teacher-recorded attendance-session information.

This is different from activity-based **inferred attendance**.

> Recorded attendance is a teacher assertion.

> Inferred attendance is an interpretation of system activity.

These should not be treated as the same variable. 

---

# 15. Concept Measures

## Source example

```text
concept-measure-SYN001.json
```

Edge-LMS can calculate measures from some submitted work, including:

* matched concepts;
* missing concepts;
* concept counts;
* coverage;
* sentence count;
* model/rule provenance. 

These variables are **derived**, not directly entered by students.

Their meaning depends on the evaluation method and version.

---

# 16. Structure and Text Measures

## Source example

```text
structure-metrics.jsonl
```

Edge-LMS can derive document characteristics including:

* word counts;
* sentence counts;
* paragraph counts;
* heading counts;
* structural checks.

Other grading components can calculate measures such as:

* readability;
* vocabulary measures;
* coherence;
* concept coverage. 

These measures can be useful as ML variables, but they are measurements produced by a particular algorithm.

They are not direct measurements of:

* intelligence;
* effort;
* ability;
* motivation.

---

# 17. Announcements and Feedback

## Source example

```text
announcement-SYN001.json
```

Edge-LMS can record:

* whether an announcement was read;
* read time;
* acknowledgement;
* archive state.

Grade records can also contain feedback-view information.

These represent **system interactions**.

For example:

> `read = true` does not prove that a student understood the announcement.

---

# 18. Risk and Similarity Data

The operational system can calculate:

* similarity between submissions;
* risk scores;
* inactivity indicators;
* `WATCH`;
* `AT_RISK`;
* inferred attendance.

These are **algorithmic or rule-based interpretations**.

They are not verified facts about students. 

They should normally be excluded from ordinary ML projects.

A suitable use could instead be an ethics exercise examining why an algorithmic classification may be misleading.

---

# 19. What Does One Record Represent?

This must always be established before analysis.

| Dataset          | Possible unit of observation            |
| ---------------- | --------------------------------------- |
| Students         | one student                             |
| Groups           | one membership                          |
| Activity         | one event or one student-period summary |
| Task attempts    | one task attempt                        |
| Quiz attempts    | one quiz attempt                        |
| Exam attempts    | one exam attempt                        |
| Grades           | one grade observation                   |
| Concept measures | one derived measurement                 |

A student may therefore occur:

* once in one dataset;
* many times in another.

This is the **grain** or **unit of observation**.

Always ask:

> **What does one row or record represent?**

---

# 20. Identifiers

The source system contains several identifiers.

Operational examples include:

* account ID;
* student number;
* course;
* module;
* submodule;
* task;
* attempt;
* group;
* exam/session identifiers.

The same identifier convention is not used everywhere. For example, group records use the student-number field while many activity records use the account/login ID. 

The teaching dataset therefore uses normalized pseudonymous identifiers such as:

```text
student_key
course_key
task_key
attempt_key
group_key
item_key
```

These allow datasets to be connected without exposing the original identities. 

An identifier tells us:

> **which entity a record belongs to**

It is not normally a numerical measurement.

---

# 21. Relationships Between Datasets

Consider:

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

The relationship is:

**one student → many quiz attempts**

After joining the datasets, `STU_A` appears twice.

Before joining data, ask:

1. What does one record represent in dataset A?
2. What does one record represent in dataset B?
3. Which identifier connects them?
4. Is the relationship one-to-one, one-to-many or many-to-many?
5. What will one row represent after the join?

---

# 22. Raw, Derived and Inferred Data

Different variables have different origins.

## Raw or directly observed

Examples:

* submitted answer;
* uploaded artifact;
* activity event;
* submission time;
* quiz response.

## Derived

Calculated from other values.

Examples:

* average quiz score;
* activity count;
* submission count;
* word count;
* concept coverage;
* days since activity.

## Inferred

Produced through rules or interpretation.

Examples:

* inferred attendance;
* `WATCH`;
* `AT_RISK`;
* similarity-risk classification.

Always ask:

> **Was this value observed, calculated or inferred?**

---

# 23. Missing Data

Missing values may have several causes.

A value may be missing because:

* the student performed no action;
* the feature was not enabled;
* the source record is unavailable;
* an older record did not contain the field;
* extraction failed;
* the field is not applicable;
* a join could not be resolved;
* the source file is missing or invalid. 

Therefore:

> **Missing does not automatically mean zero.**

The reason should be understood before values are replaced or removed.

---

# 24. Data Quality

When examining a dataset, ask:

* What does one record represent?
* What does each variable mean?
* Which fields are identifiers?
* Are technical data types correct?
* Are values missing?
* Are categories consistent?
* Are numerical ranges sensible?
* Are records duplicated?
* Are timestamps comparable?
* Can relationships be resolved?
* Is a variable raw, derived or inferred?

Do not begin machine learning before these questions have been considered.

---

# 25. Data Safety

The course uses **synthetic data by default**.

Ordinary student datasets should not contain:

* names;
* email addresses;
* real student numbers;
* operational login IDs;
* IP addresses;
* passwords or password hashes;
* reset tokens;
* sessions or cookies;
* audit/security information;
* original file paths;
* hashes;
* unreviewed teacher comments;
* raw similarity or cheating cases. 

Real student text and detailed assessment answers also require separate consideration.

Use this rule:

> **Use the data needed for the stated purpose, not every field that happens to exist.**

---

# 26. From Source Files to ML Variables

Suppose a project asks:

> **Is earlier course activity associated with later quiz performance?**

The source information might come from several places:

```text
users.json
activity-*.jsonl
quiz-related activity records
grade records
```

The project might derive variables such as:

| ML variable            | Possible source                  |
| ---------------------- | -------------------------------- |
| `student_key`          | normalized account identity      |
| `activity_count_week1` | activity logs                    |
| `days_since_activity`  | activity / last-seen information |
| `prior_attempt_count`  | quiz or grade records            |
| `later_quiz_score`     | quiz/grade records               |

The resulting analysis table might look like:

| student_key | activity_count_week1 | days_since_activity | prior_attempt_count | later_quiz_score |
| ----------- | -------------------: | ------------------: | ------------------: | ---------------: |
| STU_A       |                   14 |                   1 |                   2 |             0.82 |
| STU_B       |                    6 |                   4 |                   1 |             0.63 |
| STU_C       |                   11 |                   2 |                   1 |             0.75 |

This table does **not** exist directly in the Edge-LMS source files.

Students construct it for the analytical problem.

---

# 27. Features, Targets and Time

For supervised machine learning, distinguish between:

### Features

Information supplied to the model.

For example:

```text
prior_activity_count
previous_quiz_score
prior_submission_count
```

### Target

The value the model tries to predict.

For example:

```text
later_quiz_score
next_task_submitted
```

Time is especially important.

If the target is a result occurring at the end of Week 5, features should generally come from **before the prediction point**.

Using information collected after the outcome produces data leakage. 

---

# 28. Starting Your Project

Do not begin by choosing a machine-learning algorithm.

Use this order:

**problem → data sources → unit of analysis → variables → relationships → data quality → preparation → method**

For your project, first determine:

1. What problem are we investigating?
2. What should one observation represent?
3. Which Edge-LMS source files may contain relevant data?
4. Which variables could be useful?
5. Which variables need to be derived?
6. How can the datasets be connected?
7. What missingness or data-quality problems may matter?
8. Which fields should not be used?
9. What preprocessing is required?
10. What will the final analysis table represent?

Only then should you select an analytical or machine-learning method.

---

# 29. Project Data Workflow

```text
Project question
      ↓
Identify Edge-LMS source files
      ↓
Understand records and variables
      ↓
Select relevant fields
      ↓
Identify keys and relationships
      ↓
Read JSON / JSONL / artifacts
      ↓
Validate and clean
      ↓
Combine records
      ↓
Create derived variables
      ↓
Construct analysis-ready table
      ↓
Select features and target
      ↓
Choose method
      ↓
Analyse / model
      ↓
Validate
      ↓
Interpret
```

---

# 30. Key Principles

> **Edge-LMS data does not begin as one clean machine-learning table.**

> **Know which source files contain the information you need.**

> **Always determine what one record represents.**

> **Identifiers connect datasets but are not measurements.**

> **Understand relationships before joining data.**

> **Distinguish raw, derived and inferred variables.**

> **Missing data needs interpretation.**

> **The ML dataset is constructed for the project question.**

> **Features must be available before the outcome they are intended to predict.**

> **Not every field stored by a system should be used in analysis.**

> **Understand and prepare the data before selecting a machine-learning method.**
