---
title: "Scaling CF via CBF and Data Injection"
description: "A project on scaling CF"
summary: ""
date: 2024-12-04T17:40:15-05:00
lastmod: 2024-12-04T17:40:15-05:00
draft: false
weight: 300
seo:
  title: ""
  description: ""
  canonical: ""
  noindex: false # false (default) or true
---

{{< inline-svg "outline/leaf">}} [Overleaf Link](https://www.overleaf.com/read/wkxrbpykdpwk#e265a8) {{< inline-svg "outline/file-type-pdf">}} [Report Document](https://drive.google.com/file/d/1F24obrQb1p6QrZwRZO1xeSmJe7OpjurS/view?usp=sharing)

`2024/01-04/2024` `Python` `Recommendation systems` `LaTeX`

## Basic Info

This was a project that I worked on in the class Computational Data Analytics (ISYE-6740) at Georgia Tech's OMSA program, parterned with teamates [Garrison Winters](https://www.linkedin.com/in/garrison-winter-ms-ba389613b/), [Molly M. Bartley](https://www.linkedin.com/in/molly-bartley/).

The following is a screenshot of the report, illustrating the key ideas.

![cfcbf](images/about/cfcbf.jpg)

### The Idea

We wanted to use the basic collaborative filtering (CF) algorithm to build a book recommender system, from the famous [BookCrossing Dataset](https://www.kaggle.com/datasets/somnambwl/bookcrossing-dataset) originally collected by [Cai-Nicolas Ziegler](https://scholar.google.de/citations?user=OxRhadsAAAAJ&hl=de), and evaluate performance via n-fold cross-validated [MAE](https://en.wikipedia.org/wiki/Mean_absolute_error), [MSE](https://en.wikipedia.org/wiki/Mean_squared_error).

The problem is that the size of the dataset as well as the sparsity of the user-item matrix makes direct application of the CF algorithm to this dataset a less ideal choice. This project is an exploration of ways to scale CF to BookCrossing.

Our idea is a type of dimensionality reduction technique, using content-based filtering (CBF), with external data injected into BookCrossing. We did the following to get a reduced user-item matrix:

{{< details "Click to Expand" >}}

1. We first injected infos - including genre, summary - from a GoodReads dataset [hosted on the UCSD RecSys Repo](https://datarepo.eng.ucsd.edu/mcauley_group/gdrive/goodreads/) to BookCrossing.
1. To reduce books, we did clustering. The steps are as follows:
   - Vectorize book data (using the basic [`tfidfvectorizer`](https://scikit-learn.org/1.5/modules/generated/sklearn.feature_extraction.text.TfidfVectorizer.html))
   - Generate a K-regular graph (for some chosen K) with nodes the books, neighbors the top K similar books given by cosine similarity on these vectors (using [`NearestNeighbors`](https://scikit-learn.org/stable/modules/generated/sklearn.neighbors.NearestNeighbors.html))
   - Run Louvain community detection (using [`louvain_communities`](https://networkx.org/documentation/stable/reference/algorithms/generated/networkx.algorithms.community.louvain.louvain_communities.html)) to generated book clusters.
1. To reduce users, we did stratified subsampling. The steps are as follows:
   - We bin users into different age groups if given - this information is present in the BookCrossing dataset.
   - Inside each bin, we use the same clustering process (community detection on KNN graphs on vector representations) for users, where the vectors are defined as vector of genre counts, an info derived from the GoodReads dataset.
   - For each cluster in each bin, we choose a sampling rate according to a heuristic we defined.
1. We then derive the new user-item matrix via these subsampled users and clustered books.
   {{< /details >}}

The before-and-after after this reduction is given in the following table:

| |#U|#I|#R|#R/#U#I|
|:-:|:-:|:-:|:-:|:-:|
|B|7.69e+4|1.09e+5|7.35e+5|8.79e-5|
|A|6.84e+3|6.58e+3|8.83e+4|1.96e-3|
|A/B|8.89e-2|6.05e-2|1.20e-1|2.23e+1|

(A: After, B: Before, U: Users, I: Items, R: Ratings)

### My contributions

My contributions are summarized in the following table:

| Components | Role |
| :----------------------- | :--- |
| Modeling | Formulated main idea, coded CF algorithm |
| Data Preparation | Communicated what is needed for modeling |
| EDA | None |
| Validation | Implemented 10-fold CV |
| Reporting | Combined and typesetted teammates inputs into a {{< math >}}$\LaTeX${{< /math >}} report |

### Results

We were able to reach a best 10-fold cross-validated MAE/RMSE around **0.95**, **1.37** (where the ratings are on a scale from 1 to 10), but with reduced memory usage and increasd speed in terms of predictions. Details are given in our report.

## Final Thoughts

Although CF, CBF are some of the most basic recommender algorithms, I am still pretty happy about this project 🤗 - it has some little quirky uncommon data modeling ideas, and worked pretty fine!

{{< card-grid >}}
{{< link-card title="Back to Projects Page" href="/about/projects/" >}}
{{< link-card title="Back to Resume" href="/about/resume/" >}}
{{< /card-grid >}}
