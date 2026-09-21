# Week 6 Study Package

**Preparation for Monday 7: Machine Learning and Natural Language Processing**

Expected independent study time: **approximately 28 hours**

Suggested schedule: approximately **7 hours per day from Tuesday to Friday**.

This week follows the workflow:

**problem → text data → preprocessing/tokenization → numerical representation → model → evaluation → interpretation**

The main practical task is **text classification**.

The goal is not to master modern NLP in one week. The goal is to understand how text can become machine-learning data, build one complete text-classification workflow, evaluate it correctly, and understand where classical methods fit beside embeddings, transformers and large language models.

---

# Tuesday – From Text to Machine-Learning Features

**Suggested time: ~7 h**

## 1. What is NLP? – ~1 h

Natural Language Processing (NLP) uses computational methods to work with human language.

Examples include:

- text classification;
- sentiment analysis;
- spam detection;
- information retrieval;
- named-entity recognition;
- machine translation;
- summarization;
- question answering;
- conversational systems.

In this course we concentrate on a simple but important case:

> **Given a text, predict a category.**

This connects directly with the classification workflow studied earlier.

The difference is that the original feature is now **text**, not a ready-made numerical table.

---

## 2. Text is data, but models need numbers – ~1 h

Suppose one observation contains:

`"I cannot submit my notebook because the upload fails."`

A normal machine-learning model cannot directly use this sentence as a numerical feature vector.

We need a representation.

A classical workflow is:

**raw text → tokens → vocabulary → numerical vector**

Example tokens might be:

`I`, `cannot`, `submit`, `my`, `notebook`, `because`, `the`, `upload`, `fails`

The exact tokens depend on the tokenizer.

Important:

> Tokenization is a modelling choice.

Different decisions about punctuation, capitalization, word parts and special characters can change the representation.

---

## 3. Read: Words and Tokens – ~1.5 h

Read selected parts of:

**Jurafsky & Martin – Speech and Language Processing, Chapter 2: Words and Tokens**

Main book page:

https://web.stanford.edu/~jurafsky/slp3/

Focus on:

- what a token is;
- tokenization;
- words and word parts;
- text encoding / Unicode at a conceptual level;
- why tokenization is not always as simple as splitting at spaces.

Browse the discussion of subword tokenization such as BPE.

You do **not** need to implement BPE this week.

The important idea is:

> A computer needs a defined procedure for turning text into units that can be represented and processed.

---

## 4. Bag of words – ~1 h

A simple text representation uses the vocabulary of the training documents.

Suppose the vocabulary is:

`["error", "project", "quiz", "submit"]`

Text:

`"quiz submit submit"`

could become:

`[0, 0, 1, 2]`

The order of the original words is mostly lost. We record occurrences or counts.

This is called a **bag-of-words** representation.

Advantages:

- simple;
- fast;
- understandable;
- often a strong baseline.

Limitations:

- word order is mostly lost;
- meaning and context are represented poorly;
- vocabulary can become very large;
- similar words are normally treated as different features.

---

## 5. CountVectorizer and TF-IDF – ~1.5 h

Read selected parts of the current scikit-learn documentation:

**TfidfVectorizer**

https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.TfidfVectorizer.html

Also browse the scikit-learn text examples:

https://scikit-learn.org/stable/auto_examples/text/index.html

Understand the difference between:

### Count representation

`CountVectorizer`

Records how many times vocabulary terms occur in each document.

### TF-IDF representation

`TfidfVectorizer`

Produces numerical features based on:

- how much a term occurs in a document;
- how common or rare that term is across the document collection.

High-level idea:

> A term can be more informative if it appears strongly in a particular document but is not common in almost every document.

You do not need to memorize the full TF-IDF equation.

---

## 6. Short practical check – ~1 h

Create a very small Python example.

Use 5–10 short sentences.

Try:

```python
from sklearn.feature_extraction.text import CountVectorizer, TfidfVectorizer

texts = [
    "quiz upload failed",
    "project meeting tomorrow",
    "quiz result missing",
    "project group meeting"
]

vectorizer = CountVectorizer()
X = vectorizer.fit_transform(texts)

print(vectorizer.get_feature_names_out())
print(X.toarray())
```

Then replace `CountVectorizer()` with `TfidfVectorizer()`.

Answer:

1. What does one row represent?
2. What does one column represent?
3. Why are there usually many more columns than in ordinary tabular data?
4. What information about the original sentence is lost?
5. How does the TF-IDF matrix differ from the count matrix?

---

# Wednesday – Build a Text Classification Workflow

**Suggested time: ~7 h**

## Practical Exercise: Classify Synthetic Course Messages

Work individually using:

**`synthetic-nlp-dataset.csv`**

The dataset will contain synthetic short course-related messages.

The messages are artificial. They are designed for learning NLP and classification, not for profiling real students.

The main task is:

> **Predict the message category from the message text.**

---

## Part A – Understand the data – ~1 h

Load the dataset with pandas.

Before modelling, determine:

1. What does one row represent?
2. Which column contains the raw text?
3. Which column is the target?
4. What categories are present?
5. How many observations are in each category?
6. Are there missing text values?
7. Are there duplicate messages?
8. Which columns are identifiers or context rather than text features?

Display several messages from every target category.

Ask:

> Could a human always classify every message unambiguously?

Expect some overlap and ambiguity.

---

## Part B – Split the data – ~0.5 h

Create training and test data.

Use:

```python
train_test_split(..., stratify=y, random_state=...)
```

Keep the test data unseen during model fitting.

Important:

> Learn the text vocabulary and TF-IDF weights from the **training data**, not from the full dataset.

A scikit-learn pipeline makes this easier.

---

## Part C – Baseline – ~0.5 h

Create a simple baseline using:

```python
DummyClassifier(strategy="most_frequent")
```

Ask:

> What accuracy can we obtain without reading the text at all?

This gives a reference for the real model.

---

## Part D – First text model – ~1.5 h

Build a pipeline such as:

```python
from sklearn.pipeline import make_pipeline
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.linear_model import LogisticRegression

model = make_pipeline(
    TfidfVectorizer(),
    LogisticRegression(max_iter=1000)
)
```

Fit on training text.

Predict the test labels.

Record:

- test accuracy;
- confusion matrix;
- precision / recall / F1 where useful.

Compare with the baseline.

---

## Part E – Try Multinomial Naive Bayes – ~1 h

Read the text-classification part of:

**Jake VanderPlas – In Depth: Naive Bayes Classification**

https://jakevdp.github.io/PythonDataScienceHandbook/05.05-naive-bayes.html

Focus on:

- why text produces many features;
- why Multinomial Naive Bayes is often used with text counts/frequencies;
- the example combining TF-IDF with `MultinomialNB`.

Then try:

```python
from sklearn.naive_bayes import MultinomialNB
```

Compare:

- baseline;
- Logistic Regression;
- Multinomial Naive Bayes.

Do not search extensively for the "best" classifier.

---

## Part F – Count vs TF-IDF – ~1 h

Compare at least:

1. `CountVectorizer`
2. `TfidfVectorizer`

Keep the classifier the same.

Record results in a small table:

| Representation | Classifier | Accuracy | Main observation |
| --- | --- | ---: | --- |
| Count | ... | ... | ... |
| TF-IDF | ... | ... | ... |

Ask:

> Did changing the representation matter?

---

## Part G – Inspect mistakes – ~1.5 h

Do not stop at accuracy.

Create a table containing at least:

- original message;
- actual category;
- predicted category.

Inspect incorrectly classified examples.

Choose at least **five errors**.

For each, consider:

- Is the message ambiguous?
- Are important words shared between categories?
- Is the text very short?
- Is the target label itself debatable?
- Is the model relying on a misleading word?

Write a short conclusion:

> What kinds of messages are difficult for the model?

---

# Thursday – Representation, Evaluation and Limitations

**Suggested time: ~7 h**

## 1. Revisit classification evaluation – ~1.5 h

Text classification is still classification.

Review:

- confusion matrix;
- accuracy;
- precision;
- recall;
- F1 score;
- class imbalance;
- baseline comparison.

Ask:

> Which categories are confused with each other?

A single accuracy value can hide important errors.

---

## 2. N-grams – ~1 h

A **unigram** is one token.

Examples:

`upload`

`deadline`

A **bigram** uses two adjacent tokens.

Examples:

`upload failed`

`group project`

Try:

```python
TfidfVectorizer(ngram_range=(1, 2))
```

Compare it with:

```python
TfidfVectorizer(ngram_range=(1, 1))
```

Ask:

- Does performance change?
- Does the vocabulary become larger?
- Can two-word expressions carry information that individual words lose?

Do not assume that more n-grams always improve the model.

---

## 3. Preprocessing choices – ~1 h

Investigate at least **one** choice:

- lowercase vs preserving case;
- minimum document frequency (`min_df`);
- unigram vs unigram + bigram;
- removing very common terms;
- text length;
- punctuation or spelling variation.

Do not perform preprocessing simply because it sounds reasonable.

Ask:

> What information are we removing or changing?

Modern NLP does not have one universal "clean the text" recipe.

---

## 4. Vocabulary and model interpretation – ~1 h

Inspect:

```python
vectorizer.get_feature_names_out()
```

Look at some vocabulary terms.

If you use a linear classifier, you may optionally inspect terms with large positive coefficients for particular classes.

Be careful:

> A model coefficient shows how a feature contributes to the model prediction. It does not prove that the word causes the category or reveals the writer's intention.

Use interpretation to understand model behaviour, not to make claims about people.

---

## 5. Leakage in NLP – ~1 h

Text workflows can leak information.

Examples:

- fitting `TfidfVectorizer` on all documents before the train/test split;
- including a field that contains the category name;
- including text created after the outcome;
- duplicate or nearly identical texts appearing in both train and test;
- metadata that directly reveals the label.

Correct workflow:

**split → fit vectorizer on training text → transform training/test → fit model → evaluate**

A pipeline helps enforce this.

Investigate your dataset for possible duplicate texts.

---

## 6. Privacy, ethics and meaning – ~1 h

Text can be more sensitive than ordinary numerical columns.

A text field may contain:

- names;
- contact information;
- personal circumstances;
- opinions;
- health or family information;
- information about other people.

Before using real text, ask:

1. Why are we processing this text?
2. Do we need the complete text?
3. Who is allowed to access it?
4. How long should it be stored?
5. Could results harm or unfairly label an individual?
6. Is the model being used for a purpose different from the reason the text was collected?

For this course practical, use the **synthetic dataset**.

Do not interpret text classification as a measurement of student personality, motivation or ability.

---

## 7. Short reflection – ~0.5 h

Answer briefly:

1. What information does TF-IDF preserve?
2. What information does it mostly lose?
3. Why can a simple TF-IDF model still work well?
4. What did the model misunderstand?
5. What would make you distrust a very high test score?

---

# Friday – Modern NLP, Project Connection and Preparation for Monday

**Suggested time: ~7 h**

## 1. Where does this workflow fit in modern NLP? – ~1.5 h

The practical this week uses a classical representation:

**tokens → sparse numerical features → classifier**

Modern NLP also uses learned representations.

Read/browse from the current Jurafsky & Martin book:

https://web.stanford.edu/~jurafsky/slp3/

Browse:

- **Chapter 5: Embeddings**
- the introductory material on transformers / pretrained language models.

Understand only the high-level progression:

### Bag of words / TF-IDF

Each document becomes a sparse vector based largely on vocabulary occurrences.

### Embeddings

Words, tokens or documents can be represented by learned dense numerical vectors.

### Transformers and pretrained language models

Models can represent tokens using their context and can be pretrained on large text collections.

### Large language models

Large pretrained models can perform or support many language tasks through generation, prompting, fine-tuning or other adaptation.

You do **not** need to implement a transformer or LLM this week.

The purpose is to understand:

> TF-IDF classification is not "all of NLP"; it is a useful, transparent baseline that demonstrates the complete machine-learning workflow with text.

---

## 2. Connect NLP to your project – ~2 h

Work with your project group.

Do **not** assume that NLP belongs in your project.

Discuss:

### Text source

Does your project contain a meaningful text source?

Examples might include:

- task answers;
- feedback;
- discussion text;
- support requests;
- learning diary text.

### Unit of analysis

What would one observation represent?

Examples:

- one message;
- one answer;
- one document;
- one student-week collection of text.

### NLP task

What would you actually want to do?

Examples:

- classify messages;
- search or retrieve relevant text;
- summarize collections;
- identify recurring themes.

### Target

If doing supervised text classification:

- what is the target category?
- where would the labels come from?
- are the labels reliable?

### Validation

Could similar text from the same person or same task appear in both training and test data?

Would splitting by:

- rows;
- student;
- task;
- time

better match the intended use?

### Ethics and privacy

Would using the text be justified?

Could it contain unnecessary personal information?

Would automated interpretation create unfair labels?

If NLP does not help the project:

> **Do not force NLP into the project.**

Update the project plan only where NLP is relevant.

---

## 3. Concept map – ~1.5 h

Prepare your individual Week 6 concept map.

Choose concepts you find important, difficult, surprising or strongly connected.

Possible concepts:

- Natural Language Processing
- Text
- Document
- Token
- Tokenization
- Vocabulary
- Bag of Words
- CountVectorizer
- TF-IDF
- TfidfVectorizer
- Sparse Matrix
- N-gram
- Text Classification
- Baseline
- Logistic Regression
- Multinomial Naive Bayes
- Confusion Matrix
- Data Leakage
- Embedding
- Transformer
- Large Language Model
- Privacy

Do not try to include all of them.

Show meaningful relationships.

---

## 4. Preparation quiz – ~1 h

Complete the Week 6 theory quiz.

Topics may include:

- NLP tasks;
- tokenization;
- vocabulary;
- bag-of-words representation;
- counts vs TF-IDF;
- sparse text features;
- n-grams;
- text classification workflow;
- train/test split;
- baseline;
- evaluation;
- leakage;
- limitations of text representations;
- embeddings / transformers at a conceptual level;
- privacy and ethical use of text.

---

## 5. Practical verification – ~0.5 h

Complete the practical verification based on `synthetic-nlp-dataset.csv`.

You may need values such as:

- number of documents;
- number of target classes;
- class frequencies;
- training/test size;
- vocabulary size for a specified vectorizer;
- baseline result;
- selected model result;
- confusion-matrix values.

Use the exact workflow specified in the verification instructions.

---

## 6. Review and technical catch-up – ~0.5 h

Use the remaining time to:

- finish the notebook;
- review unclear NLP concepts;
- check classification mistakes;
- compare findings with your group;
- prepare questions for Monday.

---

# What to Submit Before Monday 7

## 1. Week 6 NLP Practical

**Individual – mandatory – PASS / REVISE / MISSING**

Submit the completed Jupyter notebook.

It should show:

- description of the problem and one observation;
- text column and target;
- class distribution;
- train/test split;
- baseline;
- text vectorization;
- at least one real classifier;
- CountVectorizer vs TF-IDF comparison;
- evaluation using appropriate classification metrics;
- inspection of misclassified texts;
- one preprocessing or n-gram experiment;
- leakage considerations;
- limitations and interpretation.

---

## 2. Week 6 Concept Map

**Individual – mandatory – PASS / REVISE / MISSING**

Submit the Week 6 concept map.

---

## 3. Project NLP Review

**Group work**

Record briefly:

- whether NLP is relevant to your project;
- possible text source and unit of analysis;
- possible NLP task;
- privacy / ethical concerns;
- validation issue if modelling text.

It is acceptable to conclude:

> NLP is not appropriate for our project.

---

## 4. Week 6 Theory Quiz

Complete the automatically graded theory quiz.

---

## 5. Week 6 Practical Verification

Complete the automatically graded practical verification.

---

# Ready for Monday 7

Before Monday you should be able to explain:

- what NLP means in this course;
- what a token and vocabulary are;
- why text must be represented numerically for classical ML;
- the basic idea of bag of words;
- the basic difference between counts and TF-IDF;
- what an n-gram is;
- how to build a text-classification pipeline;
- why a baseline is needed;
- how to evaluate text classification;
- how text preprocessing can change results;
- how leakage can occur in an NLP workflow;
- why text data raises privacy and ethical concerns;
- at a high level, how TF-IDF differs from embeddings and modern pretrained language models.

You should also have built and evaluated a complete text-classification workflow yourself.

**Monday 7 will use this knowledge for deeper NLP investigation, model-error analysis and project support rather than repeat the basic theory.**
