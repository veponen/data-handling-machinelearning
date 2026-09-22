# Monday 7 – NLP Investigation

Use your Week 6 NLP notebook and:

**`synthetic-nlp-dataset.csv`**

You already built a complete text-classification workflow during independent study.

Today, do **not** repeat the whole notebook.

Instead, investigate **one question more deeply**.

---

## Choose one investigation

Possible questions:

- Does `CountVectorizer` or `TfidfVectorizer` work better here?
- Do bigrams improve the result?
- How does Logistic Regression compare with Multinomial Naive Bayes?
- What changes if exact duplicate messages are removed?
- What changes if training and test data are split by `student_key` instead of randomly by row?
- What changes if earlier course weeks are used to predict later weeks?
- Which classes are confused most often?
- Why did the model misclassify five selected messages?
- What happens with very short or ambiguous messages?
- Which terms most strongly influence one class in Logistic Regression?
- What changes if you adjust one vectorizer setting such as `min_df`?
- Your own justified NLP question.

Choose **one** main question.

---

## Work structure

### 1. State the question

Write one clear sentence.

Example:

> Does adding bigrams improve classification of the synthetic course messages?

---

### 2. Run the experiment

Change **one main thing**.

Keep the rest of the workflow as similar as possible.

Examples:

- representation;
- classifier;
- split strategy;
- duplicate handling;
- one vectorizer setting.

---

### 3. Show evidence

Use evidence such as:

- accuracy;
- confusion matrix;
- precision / recall / F1;
- vocabulary size;
- number of duplicate messages;
- a small comparison table;
- selected misclassified messages.

Do not report only one score if another result helps explain what happened.

---

### 4. Interpret the result

Answer briefly:

- What changed?
- Why might it have changed?
- Which errors remain?
- Can you trust the comparison?
- What limitation should be mentioned?

---

# Error analysis option

If you choose misclassification analysis:

1. select at least **five wrong predictions**;
2. show the message, actual class and predicted class;
3. explain why each message may be difficult;
4. decide whether the problem is mainly:
   - representation;
   - model;
   - data;
   - target-label ambiguity.

Do not assume every wrong prediction is simply a bad model.

---

# Validation option

If you investigate splitting or duplicates, explain:

> What real-world use does this evaluation simulate?

For example:

- random row split;
- unseen-student split;
- earlier-to-later time split.

A different split can answer a different question.

---

# Group discussion

At the end, be ready to explain to your group:

1. **Question**
2. **Experiment**
3. **Evidence**
4. **Conclusion**
5. **Open question or limitation**

Keep this short.

---

# Main reminder

Return to these five questions:

1. **What exactly are we predicting?**
2. **How was the text represented?**
3. **What did the model get wrong?**
4. **Can we trust the evaluation?**
5. **Is this use of text appropriate?**

The goal is **not to obtain the highest accuracy**.

The goal is to understand what changed and whether the result deserves trust.
