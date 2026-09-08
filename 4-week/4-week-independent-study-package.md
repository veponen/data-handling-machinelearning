# Week 4 Study Package

**Preparation for Monday 5: Association Analysis**

Expected independent study time: **approximately 28 hours**

Suggested schedule: approximately **7 hours per day from Tuesday to Friday**.

This week follows the association-analysis workflow:

**problem → transactions → items → frequent itemsets → association rules → evaluate → filter → interpret**

The goal is not to generate as many rules as possible. The goal is to find and critically interpret **patterns of co-occurrence**.

Association analysis differs from the previous methods:

- **classification:** predict a known class;
- **clustering:** group similar observations;
- **association analysis:** find items, events or conditions that occur together.

A central warning for the whole week:

> **Association does not imply causation.**

---

# Tuesday – Association Analysis Concepts and Python Tools

**Suggested time: ~7 h**

## 1. Course introduction: from transactions to rules – ~1.5 h

### Transaction

A transaction is one case containing a set of items.

Examples:

- one shopping basket containing purchased products;
- one quiz attempt containing selected/correct items;
- one student-week containing selected categorical events;
- one session containing actions that occurred.

Before analysing anything, ask:

> **What exactly does one transaction represent?**

### Item and itemset

An **item** is something that can occur in a transaction.

An **itemset** is a set of items occurring together.

Example:

`{quiz_completed, concept_map_submitted}`

A frequent itemset is an itemset that occurs often enough according to a chosen **minimum support**.

### Association rule

A rule has the form:

`A → B`

For example:

`{quiz_completed} → {task_submitted}`

The left side is the **antecedent**.

The right side is the **consequent**.

The rule means that B often occurs in transactions containing A.

It does **not** mean that A causes B.

### Support

Support tells us how common an itemset is in all transactions.

If 30 of 100 transactions contain both A and B:

`support(A,B) = 30 / 100 = 0.30`

### Confidence

Confidence asks:

> Among transactions containing A, how often do we also see B?

If 40 transactions contain A and 30 contain both A and B:

`confidence(A → B) = 30 / 40 = 0.75`

### Lift

Confidence can be misleading when B is already very common.

Suppose B occurs in 50 of 100 transactions:

`support(B) = 0.50`

Then:

`lift(A → B) = 0.75 / 0.50 = 1.5`

Interpretation:

- **lift > 1:** A and B occur together more often than expected from their individual frequencies;
- **lift ≈ 1:** little evidence of association beyond their individual frequencies;
- **lift < 1:** they occur together less often than expected.

Lift still does not establish causation.

## 2. Zaki & Meira – Itemset Mining – ~2.5 h

Study selected parts of:

**Zaki & Meira – Chapter 8: Itemset Mining**

Focus on:

- transaction data;
- items and itemsets;
- support;
- frequent itemsets;
- association rules;
- confidence;
- minimum support and minimum confidence;
- the main idea of Apriori.

You do not need to reproduce the algorithm mathematically.

Understand the important Apriori principle:

> If an itemset is not frequent, adding more items cannot make it frequent.

This allows large parts of the possible itemset search space to be discarded.

Browse the other itemset-mining algorithms to understand that Apriori is not the only possible method.

## 3. mlxtend practical tools – ~2 h

We will use **mlxtend** for practical work.

If necessary, install it in your Python environment:

`%pip install mlxtend`

Study:

### TransactionEncoder

Understand how transaction lists can be transformed into a one-hot encoded Boolean table.

Example idea:

`['quiz_completed', 'task_submitted']`

becomes a row where those item columns are `True`.

### Apriori

Focus on:

- input format;
- `min_support`;
- `use_colnames=True`;
- returned frequent itemsets.

### Association rules

Focus on:

- antecedents;
- consequents;
- support;
- confidence;
- lift;
- filtering rules using thresholds.

Do not try to master all available rule metrics this week.

## 4. Short practical check – ~1 h

In Jupyter:

1. Create a very small list of transactions.
2. Convert it to a one-hot encoded DataFrame using `TransactionEncoder`.
3. Run `apriori()`.
4. Inspect the frequent itemsets.
5. Generate association rules.
6. Inspect support, confidence and lift.

Make sure you can explain what one transaction represents.

---

# Wednesday – Build an Association-Analysis Workflow

**Suggested time: ~7 h**

## Practical Exercise: Discover Association Rules

Work individually in Jupyter using:

**`synthetic-association-dataset.csv`**

The purpose is to create, evaluate and interpret association rules.

## Part A – Understand the transactions

Before running an algorithm, determine:

1. What does one transaction represent?
2. What are the possible items?
3. Which columns are identifiers rather than items?
4. Are any items duplicates or inconsistent?
5. Are any values missing?
6. Are all proposed items meaningful for the question?

Write your answers briefly in the notebook.

## Part B – Prepare transaction data

Transform the dataset into a transaction representation suitable for association analysis.

Depending on the dataset structure, this may require:

- grouping rows belonging to the same transaction;
- creating lists of items;
- removing identifiers from the item list;
- checking duplicate items;
- converting transactions into a one-hot encoded Boolean DataFrame.

Inspect the resulting table before mining patterns.

Answer:

> What does `True` in one item column mean?

## Part C – Find frequent itemsets

Use `apriori()`.

Start with a reasonable minimum support, for example:

`min_support=0.10`

Use:

`use_colnames=True`

Inspect:

- number of frequent itemsets;
- support;
- itemset length;
- most common single items;
- frequent combinations.

Try at least two different support thresholds.

Answer:

> What happens to the number of frequent itemsets when minimum support is lowered?

## Part D – Generate association rules

Use `association_rules()`.

Inspect at least:

- antecedents;
- consequents;
- support;
- confidence;
- lift.

Create a smaller table containing rules that appear potentially interesting.

Do not simply print hundreds of rules.

## Part E – Interpret rules

Select at least **three rules**.

For each rule, write:

1. What does the antecedent mean?
2. What does the consequent mean?
3. What is the support?
4. What is the confidence?
5. What is the lift?
6. What can you reasonably conclude?
7. What can you **not** conclude?

Remember:

> A rule describes co-occurrence in this dataset. It does not prove cause and effect.

---

# Thursday – Rule Quality, Thresholds and Limitations

**Suggested time: ~7 h**

## 1. Pattern and rule assessment – ~2 h

Study selected parts of:

**Zaki & Meira – Chapter 12: Pattern and Rule Assessment**

Focus especially on the purpose of measures used to assess patterns and rules.

For this course, concentrate mainly on:

- support;
- confidence;
- lift.

You do not need to reproduce the advanced statistical derivations.

Think about this problem:

> A rule can have high confidence simply because its consequent is very common.

This is one reason to examine lift rather than confidence alone.

## 2. Threshold sensitivity – ~2 h

Using your notebook, compare several settings.

For example, change:

- minimum support;
- minimum confidence;
- minimum lift.

Record how the results change.

Create a small table such as:

| Setting | Frequent itemsets | Rules | Main observation |
|---|---:|---:|---|
| A | | | |
| B | | | |
| C | | | |

Answer:

- What happens when support is lowered?
- Do very rare rules appear?
- What happens when confidence is increased?
- Which rules disappear when you require lift greater than 1?
- Can a rule be statistically interesting but practically unimportant?

The thresholds are modelling choices.

They should not be treated as natural truths hidden in the data.

## 3. Investigate a misleading rule – ~1.5 h

Find one rule that initially looks interesting but becomes less convincing after closer inspection.

Possible reasons:

- very low support;
- consequent is extremely common;
- lift is close to 1;
- the rule depends on an arbitrary category threshold;
- the transaction definition makes the pattern difficult to interpret;
- several almost identical rules describe the same basic pattern.

Record:

**Rule → why it looked interesting → additional evidence → revised interpretation**

## 4. Interpretation, validity and ethics – ~1.5 h

Answer briefly:

1. Are there enough transactions to trust rare patterns?
2. Are repeated transactions from the same synthetic student independent observations?
3. Could the way items were constructed create the association?
4. Could an association be explained by a third variable?
5. Does the dataset observe the behaviour you think it observes?
6. Could a rule lead to an unfair label about a student or group?
7. Could a small combination of items make individuals identifiable?
8. What evidence would be needed before using a rule in a real decision?

For educational data, prefer descriptions such as:

> “These recorded events frequently occurred together.”

Avoid conclusions such as:

> “Students who do A are this type of learner.”

---

# Friday – Project Connection and Preparation for Monday

**Suggested time: ~7 h**

## 1. Connect association analysis to your project – ~3 h

Work with your project group.

Do **not** assume that association analysis belongs in your project.

### Transaction

What would one transaction represent?

Possible examples:

- one student-week;
- one task attempt;
- one quiz attempt;
- one classroom session.

### Items

What events or categorical conditions could meaningfully occur in the same transaction?

Examples might include:

- task submitted;
- quiz completed;
- recorded attendance;
- multiple attempts;
- activity band;
- score band;
- concept-map submitted.

Be careful when converting numerical variables into categories.

For example:

`quiz_score > 80 → high_quiz_score`

requires you to justify why 80 is a meaningful threshold.

### Possible question

What kind of co-occurrence would actually help your project?

Example:

> Which recorded events commonly occur together?

### Interpretation

For a possible rule, ask:

- Is the rule common enough to matter?
- Is confidence high only because the consequent is common?
- What does lift show?
- Could another factor explain the association?
- Are we accidentally interpreting association as causation?

### Edge-LMS measurement limitation

Remember that the course dataset represents what Edge-LMS records.

In our course setup, ordinary student-facing Edge-LMS activity is mainly observed during Monday classroom use.

Therefore:

> lack of recorded Edge-LMS activity is not the same as lack of study activity.

### Applicability

Would association analysis actually help answer your project problem?

If not, state that clearly.

**Do not force association analysis into the project.**

Update your group's **Project Data Plan** with your conclusion.

## 2. Concept map – ~1.5 h

Prepare your individual Week 4 concept map.

Choose concepts you find important, difficult, surprising or strongly connected.

Possible concepts include:

- Association Analysis
- Transaction
- Item
- Itemset
- Frequent Itemset
- Association Rule
- Antecedent
- Consequent
- Support
- Confidence
- Lift
- Minimum Support
- Apriori
- One-hot Encoding
- Rule Filtering
- Association vs Causation
- Interpretation

Do not try to include all of them.

Show meaningful relationships.

## 3. Preparation quiz – ~1 h

Complete the Week 4 theory quiz.

Topics may include:

- transactions and items;
- frequent itemsets;
- support;
- antecedent and consequent;
- confidence;
- lift;
- Apriori;
- minimum support;
- transaction encoding;
- rule filtering;
- threshold sensitivity;
- interpretation;
- association vs causation;
- appropriate use of association analysis.

## 4. Practical verification – ~0.5 h

Complete the practical verification task based on your notebook.

You may need values such as:

- number of transactions;
- number of unique items;
- selected minimum-support threshold;
- number of frequent itemsets;
- number of generated rules;
- support, confidence and lift of selected rules.

## 5. Review and technical catch-up – ~1 h

Use the remaining time to:

- finish the notebook;
- correct technical problems;
- review unclear concepts;
- compare findings with your group;
- prepare questions for Monday.

---

# What to Submit Before Monday 5

## 1. Week 4 Association-Analysis Practical

**Individual – mandatory – PASS / REVISE / MISSING**

Submit your completed Jupyter notebook.

It should show:

- definition of one transaction;
- identification of items;
- transaction preparation;
- one-hot encoding;
- frequent-itemset mining with Apriori;
- comparison of support thresholds;
- association-rule generation;
- support, confidence and lift;
- interpretation of at least three rules;
- investigation of one potentially misleading rule;
- interpretation and limitations.

The teacher may ask you to explain or demonstrate any part of the work.

## 2. Week 4 Concept Map

**Individual – mandatory – PASS / REVISE / MISSING**

Submit your Week 4 concept map.

## 3. Week 4 Project Data Plan Update

**Group work**

Update the shared Project Data Plan with your association-analysis discussion:

- possible transaction;
- possible items;
- useful association question;
- possible categorisation choices;
- interpretation risks;
- whether association analysis is appropriate for the project.

## 4. Week 4 Theory Quiz

Complete the automatically graded theory quiz.

## 5. Week 4 Practical Verification

Complete the automatically graded practical verification task.

---

# Ready for Monday 5

Before Monday you should be able to explain:

- how association analysis differs from classification and clustering;
- what a transaction represents;
- what items and itemsets are;
- what makes an itemset frequent;
- what antecedent and consequent mean;
- what support measures;
- what confidence measures;
- why confidence alone can be misleading;
- what lift tells you;
- the basic idea of Apriori;
- why thresholds affect the rules you obtain;
- why numerical variables may need meaningful categorisation;
- why association does not imply causation;
- why a strong-looking rule may still be unimportant or misleading.

You should also have built and interpreted a complete association-analysis workflow yourself.

**Monday 5 will use this knowledge for deeper association-analysis work and project support, not repeat the basic theory.**

---

# Source links

- Zaki & Meira online book: https://dataminingbook.info/book_html/
- Chapter 8 – Itemset Mining: https://dataminingbook.info/book_html/chap8/book.html
- Chapter 12 – Pattern and Rule Assessment: https://dataminingbook.info/book_html/chap12/book.html
- mlxtend TransactionEncoder: https://rasbt.github.io/mlxtend/user_guide/preprocessing/TransactionEncoder/
- mlxtend Apriori: https://rasbt.github.io/mlxtend/user_guide/frequent_patterns/apriori/
- mlxtend association_rules: https://rasbt.github.io/mlxtend/user_guide/frequent_patterns/association_rules/
