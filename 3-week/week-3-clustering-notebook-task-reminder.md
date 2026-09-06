# Week 3 Clustering Notebook

**Individual task**

Use:

* `synthetic-clustering-dataset.csv`
* Jupyter Notebook
* the Week 3 study material

The purpose is to build and interpret a complete clustering workflow.

## 1. Understand the data

Answer briefly:

* What does one observation represent?
* Which variables could meaningfully describe similarity?
* Which variables should not be used as clustering features?
* Are there identifiers?
* Are there missing values?
* Are the numerical scales very different?

## 2. Prepare the features

Create the feature matrix `X`.

* Select suitable numerical features.
* Handle missing values.
* Standardize the numerical features.
* Record which features you included and why.

## 3. Run k-means

Start with a small number of clusters, for example:

```python
KMeans(n_clusters=3, random_state=...)
```

Inspect:

* cluster labels
* cluster sizes
* cluster centers

Remember: cluster labels such as `0`, `1` and `2` are identifiers, not rankings.

## 4. Describe the clusters

For each cluster, calculate useful summaries using the original variables.

For example:

| Cluster | Size | Mean quiz score | Mean attempts | Mean activity |
| ------- | ---: | --------------: | ------------: | ------------: |
| 0       |      |                 |               |               |
| 1       |      |                 |               |               |
| 2       |      |                 |               |               |

Explain:

* how the clusters differ
* which variables seem important
* whether some clusters are very small
* whether the groups are easy or difficult to interpret

Describe measured differences.

Avoid unsupported labels such as:

* “good students”
* “weak students”
* “motivated students”

## 5. Visualize

Create at least one useful visualization.

For example:

* scatter plot with cluster colours
* feature distributions by cluster
* cluster-center comparison

## 6. Compare different numbers of clusters

Try several values, for example:

```text
k = 2, 3, 4, 5, 6
```

For each value, record:

* cluster sizes
* silhouette score
* main observation

Do not assume that there is one automatically correct value of `k`.

## 7. Test the effect of scaling

Run clustering:

1. without scaling
2. with scaling

Compare the results.

Explain:

* whether cluster membership changed
* which variables may have dominated without scaling
* why scaling affected, or did not affect, the result

## 8. Compare with hierarchical clustering

Use `AgglomerativeClustering` with the same prepared features.

Compare briefly with k-means:

* Which observations stay together?
* Which observations move?
* Are the resulting groups easier or harder to interpret?

## 9. Interpretation and limitations

Answer briefly:

* Which clustering solution seems most useful?
* Why?
* Are the clusters clearly separated?
* Would another reasonable feature selection change the result?
* Could another algorithm produce different groups?
* What can you safely conclude from the clusters?
* What should you avoid concluding?

## Submit

Submit the completed `.ipynb` notebook.

It should show:

* unit of analysis
* feature selection
* preprocessing and scaling
* k-means
* several values of `k`
* cluster descriptions
* visualization
* silhouette comparison
* scaled vs unscaled comparison
* hierarchical clustering comparison
* interpretation and limitations


