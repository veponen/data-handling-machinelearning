# Week 3 Study Package

**Preparation for Monday 4: Clustering**

Expected independent study time: **approximately 28 hours**

Suggested schedule: approximately **7 hours per day from Tuesday to Friday**.

This week follows the clustering workflow:

**problem → observations → features → preprocessing/scaling → similarity → clustering → validation → visualization → interpretation**

The goal is not to learn many clustering algorithms. The goal is to understand **how groups can be discovered from data and how cautiously those groups must be interpreted**.

Unlike classification, clustering normally has **no target variable `y`**.

---

# Tuesday – Clustering, Similarity and Scaling

**Suggested time: ~7 h**

## 1. Clustering concepts – ~2 h

Study:

### Jake VanderPlas – What Is Machine Learning?

Focus on the section:

**Clustering: Inferring labels on unlabeled data**

Clustering is an unsupervised learning task: the algorithm looks for structure in the features without known target labels.

[VanderPlas – What Is Machine Learning?](https://jakevdp.github.io/PythonDataScienceHandbook/05.01-what-is-machine-learning.html?utm_source=chatgpt.com)

Then study:

### Jake VanderPlas – In Depth: k-Means Clustering

Focus especially on:

* what a cluster represents;
* cluster centers;
* assignment based on distance;
* the iterative k-means process;
* why the number of clusters must be chosen;
* limitations of k-means;
* why different initializations can matter.

[VanderPlas – In Depth: k-Means Clustering](https://jakevdp.github.io/PythonDataScienceHandbook/05.11-k-means.html?utm_source=chatgpt.com)

Do not concentrate on reproducing every mathematical detail.

---

## 2. Zaki & Meira – representative-based clustering – ~2 h

Study selected parts of:

**Chapter 13: Representative-based Clustering**

Concentrate on:

* Section 13.1: K-means;
* observations represented by multiple features;
* distance from observations to cluster representatives;
* how cluster representatives are updated.

Browse the later parts of the chapter to understand that k-means is only one approach to clustering. Zaki & Meira place k-means in Chapter 13 and hierarchical clustering in Chapter 14.

[Zaki & Meira – Online Book](https://dataminingbook.info/book_html/?utm_source=chatgpt.com)

---

## 3. Scaling and distance – ~2 h

Return to the question:

> **What does it mean for two observations to be similar?**

Consider a dataset containing:

| Variable       | Typical values |
| -------------- | -------------: |
| quiz score     |          0–100 |
| task attempts  |            0–5 |
| activity count |           0–30 |

If Euclidean distance is calculated directly, variables with larger numerical ranges can dominate the result.

Study the scikit-learn description of `StandardScaler`.

Standardization removes the mean and scales features according to their standard deviation.

[scikit-learn – StandardScaler](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.StandardScaler.html?utm_source=chatgpt.com)

Think about:

* Why can scaling change clusters?
* Should identifiers be included as features?
* What about categorical variables?
* Does numerical storage mean that distance is meaningful?

Connect this with the earlier course work on **semantic data types**.

---

## 4. Short practical check – ~1 h

In Jupyter:

1. Load a small numerical dataset.
2. Identify the observations.
3. Select two or three numerical features.
4. Inspect their ranges.
5. Standardize the features.
6. Fit `KMeans`.
7. Add the resulting cluster label to a copy of the data.
8. Count the observations in each cluster.

Do not try to decide whether the clusters are "correct" yet.

---

# Wednesday – Build a Clustering Workflow

**Suggested time: ~7 h**

## Practical Exercise: Discover and Describe Clusters

Work individually using the provided **synthetic clustering dataset**.

---

## Part A – Understand the problem

Before clustering, answer:

1. What does one observation represent?
2. Which variables describe that observation?
3. Which variables could meaningfully contribute to similarity?
4. Which variables should not be features?
5. Are any variables identifiers?
6. Are any variables outcomes that would dominate the interpretation?
7. Are there missing values?
8. Are numerical feature scales very different?

Remember:

> Clustering groups observations according to the features you choose.

Changing the features can change the meaning of the clusters.

---

## Part B – Prepare the features

Create the feature matrix `X`.

Handle:

* missing values;
* inappropriate variables;
* numerical types;
* scaling.

Keep a record of which variables you included and why.

Create a standardized version of the numerical features.

---

## Part C – Run k-means

Start with a reasonable small value such as:

```python
KMeans(n_clusters=3, random_state=...)
```

Use reproducible settings.

Inspect:

* cluster labels;
* number of observations per cluster;
* cluster centers.

Remember:

> Cluster labels such as `0`, `1` and `2` are identifiers, not rankings.

Cluster 2 is not automatically "better" or "higher" than cluster 1.

---

## Part D – Describe the clusters

For each cluster, calculate useful summaries of the **original variables**.

For example:

| Cluster | Size | Mean quiz score | Mean attempts | Mean activity |
| ------- | ---: | --------------: | ------------: | ------------: |

Ask:

* How are the clusters different?
* Which variables seem to distinguish them?
* Are differences large or small?
* Is any cluster very small?
* Are the observations within each cluster actually similar?

Do not immediately give clusters names such as:

* "good students";
* "weak students";
* "motivated students".

Describe the **observed variables**, not assumed personal characteristics.

---

## Part E – Visualize

Create at least one useful visualization.

Possible examples:

* scatter plot using two selected features;
* cluster-colored scatter plot;
* cluster-center comparison;
* box plots of important variables by cluster.

Remember that a two-dimensional plot shows only part of a multidimensional clustering result.

---

## Part F – Change the number of clusters

Try several values, for example:

```text
k = 2, 3, 4, 5, 6
```

Record:

* cluster sizes;
* important changes;
* whether some solutions seem more interpretable than others.

Do not assume that there is one objectively correct `k`.

---

# Thursday – Validation, Sensitivity and Alternative Clustering

**Suggested time: ~7 h**

## 1. Clustering validation – ~2 h

Clustering usually does not have known correct target labels.

Therefore evaluation differs from classification.

Study the scikit-learn example:

### Selecting the number of clusters with silhouette analysis

The silhouette coefficient considers both:

* similarity to observations in the same cluster;
* separation from the nearest other cluster.

Values closer to 1 indicate better separated/cohesive clusters, values near 0 indicate overlap, and negative values can indicate questionable assignment.

[scikit-learn – Silhouette analysis with KMeans](https://scikit-learn.org/stable/auto_examples/cluster/plot_kmeans_silhouette_analysis.html?utm_source=chatgpt.com)

### Practical work

For several values of `k`:

1. calculate the silhouette score;
2. record cluster sizes;
3. inspect the visualization;
4. inspect cluster summaries.

Create a table such as:

|  k | Silhouette score | Cluster sizes | Main observation |
| -: | ---------------: | ------------- | ---------------- |

Then answer:

> Which clustering appears most useful, and why?

Do not choose only from one number.

---

## 2. Scaling sensitivity – ~1.5 h

Run clustering:

1. without scaling;
2. with scaling.

Compare:

* cluster membership;
* cluster sizes;
* cluster centers/profiles;
* silhouette scores.

Answer:

> Why did scaling change, or not change, the result?

Identify which variables dominated the unscaled distances.

---

## 3. Hierarchical clustering – ~1.5 h

Browse:

**Zaki & Meira – Chapter 14: Hierarchical Clustering**

Focus especially on:

* the idea of progressively joining observations/groups;
* agglomerative hierarchical clustering;
* the fact that clustering can be represented as a hierarchy rather than only one fixed partition.

Use scikit-learn `AgglomerativeClustering` to create one alternative clustering from the same prepared features.

You do not need to explore every linkage method.

Compare briefly with k-means:

* Are similar observations grouped together?
* Which observations change groups?
* Does one method produce a more interpretable result?

The purpose is comparison, not finding a universal winner.

---

## 4. Interpretation and limitations – ~1 h

Answer briefly:

1. Do the clusters seem clearly separated?
2. Would another reasonable feature selection produce different clusters?
3. Would another scaling choice affect the result?
4. Are the cluster labels meaningful outside this dataset?
5. Is there enough data to make strong conclusions?
6. Could the clusters encourage misleading labels about people?
7. What would you investigate before using the result in a real decision?

---

## 5. Optional deeper reading – ~1 h

If you want deeper clustering material, browse:

* Zaki & Meira Chapter 15: Density-based Clustering;
* Zaki & Meira Chapter 17: Clustering Validation.

These chapters introduce alternatives to representative-based clustering and more formal ways to assess clustering results.

Do not try to master all methods this week.

---

# Friday – Project Connection and Preparation for Monday

**Suggested time: ~7 h**

## 1. Connect clustering to your project – ~3 h

Work with your project group.

Do **not** assume that clustering belongs in your project.

Discuss:

### Unit of analysis

What would one clustered observation represent?

Examples:

* one student;
* one student-week;
* one task attempt;
* one document.

### Purpose

What would clustering help you understand?

For example:

> Are there observations with similar patterns across several variables?

### Features

Which variables should determine similarity?

For each proposed feature ask:

> Why should similarity on this variable matter to our project question?

### Scaling

Are the variables on different scales?

Would scaling be necessary?

### Interpretation

If clusters appear, what could you safely say about them?

Avoid turning mathematical clusters into unsupported labels about people.

### Applicability

Would clustering actually help answer the project problem?

If not, state that clearly.

**Do not force clustering into the project.**

Update your group's **Project Data Plan** with your conclusions.

---

## 2. Concept map – ~1.5 h

Prepare your individual Week 3 concept map.

Choose concepts you find important, difficult, surprising or strongly connected.

Possible concepts include:

* Clustering
* Unsupervised Learning
* Observation
* Feature
* Similarity
* Distance
* Scaling
* Standardization
* K-Means
* Cluster Center
* Cluster Label
* Number of Clusters
* Silhouette Score
* Hierarchical Clustering
* Interpretation

Do not try to include all of them.

Show meaningful relationships.

---

## 3. Preparation quiz – ~1 h

Complete the Week 3 theory quiz.

Topics may include:

* clustering vs classification;
* unsupervised learning;
* observations and features;
* similarity and distance;
* scaling;
* k-means;
* cluster centers and labels;
* choosing number of clusters;
* silhouette score;
* hierarchical clustering;
* visualization;
* interpretation and applicability.

---

## 4. Practical verification – ~0.5 h

Complete the practical verification task based on your notebook.

You may need values such as:

* number of observations;
* selected features;
* cluster sizes;
* silhouette scores;
* results before and after scaling;
* summaries of selected clusters.

---

## 5. Review and technical catch-up – ~1 h

Use the remaining time to:

* finish the notebook;
* correct technical problems;
* review unclear clustering concepts;
* compare findings with your group;
* prepare questions for Monday.

---

# What to Submit Before Monday 4

## 1. Week 3 Clustering Practical

**Individual – mandatory – PASS / REVISE / MISSING**

Submit your completed clustering notebook.

It should show:

* unit of analysis;
* feature selection;
* preprocessing and scaling;
* k-means clustering;
* several values of `k`;
* cluster sizes and descriptions;
* visualization;
* silhouette comparison;
* scaling comparison;
* one hierarchical clustering comparison;
* interpretation and limitations.

The teacher may ask you to explain or demonstrate any part of the work.

---

## 2. Week 3 Concept Map

**Individual – mandatory – PASS / REVISE / MISSING**

Submit your Week 3 concept map.

---

## 3. Week 3 Project Data Plan Update

**Group work**

Update the shared Project Data Plan with your clustering discussion:

* possible unit of analysis;
* possible clustering purpose;
* candidate features;
* scaling considerations;
* interpretation risks;
* whether clustering is appropriate for the project.

---

## 4. Week 3 Theory Quiz

Complete the automatically graded theory quiz.

---

## 5. Week 3 Practical Verification

Complete the automatically graded practical verification task.

---

# Ready for Monday 4

Before Monday you should be able to explain:

* how clustering differs from classification;
* why clustering normally has no target variable;
* how feature selection defines similarity;
* why scaling can change a clustering result;
* what k-means does;
* what a cluster center represents;
* why cluster numbers are only labels;
* why the number of clusters must be considered carefully;
* what a silhouette score tells you;
* why visualization alone is not sufficient validation;
* how hierarchical clustering differs conceptually from k-means;
* why clusters should not automatically be interpreted as real types of people.

You should also have built, compared and interpreted a complete clustering workflow yourself.

**Monday 4 will use this knowledge for deeper clustering work and project support, not repeat the basic theory.**
