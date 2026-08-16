I would use the following as the first custom student-facing theory material. I kept it deliberately compact and focused on decisions students will soon need to make with real datasets.

# Understanding Data: Types, Meaning and Valid Operations

Before analysing data or training a machine-learning model, you need to understand **what the data represents**.

A computer can tell you how a value is stored. It cannot automatically tell you what that value means.

Consider:

```text
age = 25
customer_id = 25
satisfaction = 3
```

All three may be stored as integers, but they represent very different things.

That difference determines which operations and analyses make sense.

## 1. Technical type and meaning are different

A **technical data type** describes how data is represented by software.

Common examples are:

* integer
* floating-point number
* Boolean
* string
* datetime
* categorical

NumPy and pandas use data types to determine how values are stored and what operations can be performed on them. ([NumPy][1])

But for analysis we must also ask:

> **What does this variable actually mean?**

For example:

| Variable          | Technical type | Meaning               |
| ----------------- | -------------- | --------------------- |
| Age               | integer        | numerical measurement |
| Customer ID       | integer        | identifier            |
| City              | string         | nominal category      |
| Satisfaction 1–5  | integer        | ordinal category      |
| Registration date | datetime       | temporal data         |
| Customer review   | string         | text                  |

Therefore:

> **Never decide how to analyse a variable only from its Python or pandas data type.**

---

# 2. Nominal data

Nominal data represents **categories without a natural order**.

Examples:

* country
* city
* product category
* blood type
* colour

For nominal values, equality and difference between categories are meaningful:

```text
Helsinki == Helsinki
Helsinki != Espoo
```

But ordering is not:

```text
Helsinki < Espoo
```

and neither is arithmetic:

```text
Helsinki + Espoo
```

Assigning numbers to categories does not change this.

For example:

```text
1 = Helsinki
2 = Espoo
3 = Vantaa
```

does **not** mean that Vantaa is three times Helsinki or that Espoo lies numerically between Helsinki and Vantaa.

Typical useful operations include:

* counting;
* frequencies and proportions;
* grouping;
* mode;
* comparing whether categories are the same or different.

In pandas, categorical variables can explicitly be represented as categorical data. Categories are not ordered unless ordering is defined. ([Pandas][2])

---

# 3. Ordinal data

Ordinal data consists of categories with a **meaningful order**.

Examples:

```text
poor < satisfactory < good < excellent
```

or:

```text
low < medium < high
```

The ordering is meaningful, but the distance between categories is not necessarily equal.

For example, the difference between **poor and satisfactory** does not have to be the same as the difference between **good and excellent**.

Useful operations can include:

* equality;
* ordering;
* ranking;
* counts and proportions;
* median or other order-based summaries.

Be careful with arithmetic. A variable encoded as:

```text
1 = poor
2 = satisfactory
3 = good
4 = excellent
```

contains numbers, but this does not automatically make operations such as averaging or multiplication meaningful.

NIST describes an ordinal scale as a categorical scale with a natural order. ([NIST][3])

---

# 4. Interval data

Interval data has:

* meaningful ordering;
* meaningful differences;
* equal intervals between values.

A common example is **temperature in Celsius**.

The difference between 10 °C and 20 °C is the same size as the difference between 20 °C and 30 °C.

However:

```text
20 °C is twice 10 °C
```

is not meaningful because zero Celsius is not an absolute absence of temperature.

For interval data, differences, averages and many statistical operations can be meaningful, but ratios require care. ([NIST][3])

---

# 5. Ratio data

Ratio data has the properties of interval data plus a **meaningful zero point**.

Examples include many measurements such as:

* distance;
* duration;
* mass;
* number of purchases;
* income when zero represents no income.

With ratio data, statements such as these may be meaningful:

```text
20 kg is twice 10 kg.
```

Ratio data therefore supports the widest range of ordinary arithmetic operations.

NIST distinguishes ratio scales from interval scales by the existence of a meaningful zero. ([NIST][3])

---

# 6. Discrete and continuous data

Numerical variables can also be described as **discrete** or **continuous**.

### Discrete

Discrete data consists of separate countable values.

Examples:

* number of purchases;
* number of students;
* number of failed login attempts.

Possible values might be:

```text
0, 1, 2, 3, ...
```

but not:

```text
2.37 students
```

### Continuous

Continuous variables represent quantities that can, in principle, take values anywhere within a range.

Examples:

* height;
* weight;
* elapsed time;
* temperature.

A measurement may be stored with limited precision:

```text
175.4 cm
```

but the underlying quantity is still continuous.

**Discrete/continuous and nominal/ordinal/interval/ratio describe different aspects of data.**

---

# 7. Important special cases

## Identifiers

Examples:

```text
student_id = 204583
customer_id = 92731
postcode = 02600
```

These may be stored as numbers, but usually they are **labels identifying entities**, not measurements.

Calculating:

```text
mean(customer_id)
```

would normally have no useful meaning.

Identifiers are therefore often excluded from machine-learning features unless their structure has some separately justified meaning.

---

## Binary variables

Binary variables have two possible states:

```text
yes / no
passed / failed
fraud / not fraud
```

They are often treated as categorical variables.

Binary targets are especially common in **classification problems**.

---

## Dates and time

Dates and timestamps have their own semantics.

Useful operations include:

* ordering events;
* calculating elapsed time;
* extracting year, month, weekday or hour;
* analysing change over time.

Pandas provides dedicated datetime types and operations rather than requiring dates to be treated simply as strings. ([Pandas][4])

---

## Text

Text is not just another categorical variable.

Examples:

* customer reviews;
* messages;
* documents;
* support tickets.

Text can be searched, counted and processed using string operations. For machine learning, it normally needs to be transformed into a numerical representation suitable for the chosen method. Pandas provides dedicated operations for working with text data. ([Pandas][5])

Natural-language processing will be studied later in this course.

---

# 8. Data type determines meaningful operations

A useful first question is:

> **What operations make sense for this variable?**

| Data       | Example           | Usually meaningful                      |
| ---------- | ----------------- | --------------------------------------- |
| Nominal    | city              | equality, counts, proportions, grouping |
| Ordinal    | low/medium/high   | above + ordering and ranking            |
| Interval   | °C                | differences, averages                   |
| Ratio      | weight            | differences, ratios, arithmetic         |
| Identifier | student ID        | equality, lookup                        |
| Datetime   | registration time | ordering, durations, time components    |
| Text       | feedback          | text operations, NLP                    |
| Binary     | pass/fail         | counts, proportions, classification     |

The table is a guide, not a substitute for understanding what a particular variable represents.

---

# 9. Missing data is also information about the dataset

Real datasets often contain missing values.

A missing value does not automatically mean zero.

For example:

```text
income = missing
```

does not mean:

```text
income = 0
```

Before changing missing values, ask:

* Why is the value missing?
* Is it missing by accident?
* Does missingness itself carry information?
* Can the observation still be used?
* Can the value reasonably be estimated?

Pandas represents missing data using several missing-value representations depending on the data type. ([Pandas][6])

Machine-learning preprocessing may involve replacing missing values, for example using a median, most frequent value or another strategy. The correct choice depends on the variable and the problem; imputation should not be performed automatically without considering its meaning. ([Scikit-learn][7])

---

# 10. Data type also affects machine learning

Many machine-learning algorithms ultimately operate on numerical representations.

That does **not** mean that every variable should simply be converted to an arbitrary number.

For example, a nominal variable:

```text
city:
Helsinki
Espoo
Vantaa
```

might be represented using separate binary features rather than:

```text
Helsinki = 1
Espoo = 2
Vantaa = 3
```

Scikit-learn provides one-hot encoding specifically for converting categorical features into numerical features without introducing an artificial numerical ordering. ([Scikit-learn][8])

Ordered categories require different thinking because their ordering may contain useful information.

Therefore, preprocessing depends on:

**what the variable means → what operations are valid → what analysis or model will use it**

---

# 11. A practical decision process

When you encounter a new variable, ask:

### 1. What does it represent?

Not:

> What Python type is it?

but:

> What does this value mean in the real problem?

### 2. What type of information is it?

For example:

* nominal;
* ordinal;
* numerical measurement;
* identifier;
* datetime;
* text.

### 3. Which operations make sense?

Can you:

* compare equality?
* order values?
* calculate differences?
* calculate ratios?
* calculate averages?

### 4. Is the current representation correct?

Examples:

```text
"2026-08-16"
```

may need to become a datetime.

```text
1, 2, 3
```

may actually represent categories.

### 5. How should it be prepared?

Only then decide whether to:

* keep it;
* remove it;
* clean it;
* encode it;
* scale it;
* derive another variable from it;
* handle missing values;
* transform it for machine learning.

---

# Short exercises

## Exercise 1 — What is the data?

For each variable, identify its likely meaning and type.

| Variable          | Example                        |
| ----------------- | ------------------------------ |
| Student number    | `2518437`                      |
| Age               | `24`                           |
| Study programme   | `"ICT"`                        |
| Satisfaction      | `1–5`                          |
| Completed courses | `17`                           |
| Registration date | `"2026-08-10"`                 |
| Student feedback  | `"The exercise was difficult"` |

For each variable ask:

1. What does it represent?
2. Is it categorical, numerical, identifier, datetime or text?
3. Which operations would be meaningful?
4. Could its technical data type be misleading?

---

## Exercise 2 — Does the operation make sense?

Decide whether each operation is meaningful and explain why.

1. Mean age of students.
2. Mean student ID.
3. Most common city.
4. Highest satisfaction category.
5. Difference between two timestamps.
6. `"Helsinki" × 3`.
7. Ratio between two weights.
8. Average postcode.

---

## Exercise 3 — Find the problem

Consider:

```text
City
1 = Helsinki
2 = Espoo
3 = Vantaa
```

A program calculates:

```text
mean(City) = 2.1
```

What is wrong with interpreting this as an average city?

---

## Exercise 4 — Think before preprocessing

A dataset contains missing values in the variable:

```text
weekly_study_hours
```

Give at least three possible ways of handling the missing values.

For each method, explain one situation where it could produce a misleading result.

---

# Key idea

The most important lesson is:

> **A value's meaning determines how it should be analysed—not the way the computer happens to store it.**

Understanding the data comes before cleaning, statistical analysis and machine learning.

## Sources

This material uses terminology and technical behaviour documented by NIST for measurement scales and by the official NumPy, pandas and scikit-learn documentation for data representation and preprocessing.

[1]: https://numpy.org/doc/stable/user/basics.types.html?utm_source=chatgpt.com "Data types — NumPy v2.4 Manual"
[2]: https://pandas.pydata.org/docs/user_guide/categorical.html?utm_source=chatgpt.com "Categorical data — pandas 3.0.5 documentation - PyData |"
[3]: https://www.nist.gov/itl/ai/ai-standards-and-guidelines-group/metrics-and-measures?utm_source=chatgpt.com "Metrics and Measures | NIST"
[4]: https://pandas.pydata.org/docs/user_guide/timeseries.html?utm_source=chatgpt.com "Time series / date functionality — pandas 3.0.5 documentation"
[5]: https://pandas.pydata.org/docs/user_guide/text.html?utm_source=chatgpt.com "Working with text data — pandas 3.0.5 documentation"
[6]: https://pandas.pydata.org/docs/user_guide/missing_data.html?utm_source=chatgpt.com "Working with missing data — pandas 3.0.5 documentation"
[7]: https://scikit-learn.org/stable/modules/impute.html?utm_source=chatgpt.com "8.4. Imputation of missing values"
[8]: https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html?utm_source=chatgpt.com "OneHotEncoder — scikit-learn 1.9.0 documentation"
