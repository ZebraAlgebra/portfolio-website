---
title: "OMSA Course Review"
description: "Blog post on review of courses in OSMA"
summary: "Review of courses in OMSA."
date: 2024-11-29T13:37:28-05:00
lastmod: 2024-11-29T13:37:28-05:00
draft: false
weight: -200
categories: ["omsa"]
tags: ["review"]
contributors: []
pinned: false
homepage: false
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

I enrolled in Georgia Tech's _Online Masters in Analytics_ program as a fulltime student, starting from 2023 Fall, graduated in 2024 Fall. This blog post will be my review on these OMSA courses.

## Completed Courses

The list of courses I have taken are as follows:

| **Course #** | **Nickname** | **Semester** | **Classification** |
| -----------: | :----------: | :----------: | :----------------: |
|    `CSE6040` |     iCDA     |   🍁 23 FA   |        Core        |
|   `ISYE6501` |     iAM      |   🍁 23 FA   |        Core        |
|   `ISYE6644` |     Sim      |   🍁 23 FA   |     OR Elect.      |
|    `MGT8803` |     BFA      |   🌸 23 SP   |        Core        |
|   `ISYE6740` |     CDA      |   🌸 24 SP   |    Stat. Elect.    |
|    `MGT6203` |     DAB      |   🌸 24 SP   |     Adv. Core      |
|    `CSE6242` |     DVA      |   🌸 24 SP   |     Adv. Core      |
|   `ISYE8803` |     HDDA     |   🌻 24 SU   |    Track Elect.    |
|     `CS7280` |      NS      |   🌻 24 SU   |    Track Elect.    |
|    `CSE8803` |     ANLP     |   🍁 24 FA   |    Track Elect.    |
|    `CSE6748` |     Prac     |   🍁 24 FA   |     Practicum.     |
|    `ISYE6669` |     DO|   🌸 25 SP   |    OR Elect.    |
|    `CS7643` |     DL|   🌸 25 SP   |     Track Elect.     |

My ratings are as follows:

|                    **Name**                     | **Difficulty** | **Enjoyment** | **Workload** |
| :---------------------------------------------: | :------------: | :-----------: | :----------: |
|     [iCDA](#1-computing-for-data-analysis)      |   🟩`03/10`    |   😊`09/10`   |  🟨`05/10`   |
|  [iAM](#2-introduction-to-analytics-modeling)   |   🟨`05/10`    |   😊`08/10`   |  🟨`06/10`   |
|              [Sim](#3-simulation)               |   🟩`04/10`    |   😊`08/10`   |  🟩`04/10`   |
|  [BFA](#4-business-fundamentals-for-analytics)  |   🟥`09/10`    |   😨`04/10`   |  🟩`03/10`   |
|     [CDA](#5-computational-data-analytics)      |   🟧`07/10`    |   😊`09/10`   |  🟧`07/10`   |
|      [DAB](#6-data-analytics-in-business)       |   🟩`03/10`    |   🫢`05/10`   |  🟩`03/10`   |
|       [DVA](#7-data-and-visual-analytics)       |   🟨`05/10`    |   🫢`06/10`   |  🟥`09/10`   |
|  [HDDA](#8-higher-dimensional-data-analytics)   |   🟧`07/10`    |   🤩`10/10`   |  🟧`07/10`   |
|            [NS](#9-network-science)             |   🟩`04/10`    |   🫢`05/10`   |  🟨`05/10`   |
| [ANLP](#10-applied-natural-language-processing) |   🟩`03/10`    |   🫢`06/10`   |  🟩`04/10`   |
|     [Prac](#11-applied-analytics-practicum)     |   🟨`05/10`    |   😊`08/10`   |  🟧`07/10`   |
|    [DO](#12-deterministic-optimization) |IP|IP|IP|
|    [DL](#13-deep-learning) |IP|IP|IP|

*IP = In Progress

## Course Reviews

For what follows, DEW = Difficulty/Enjoyment/Workload ratings.

#### 1. Computing for Data Analysis

`iCDA` `CSE6040`

- **DEW**: 3/9/5
- **Format**:
  - HW: Weekly basis. All Jupyter notebooks.
  - Exams: 3 exams.
    - Open book, but no Github Copilot, posting exam questions on forums, or interacting with other people.
    - Similar to homeworks and practice problems.
  - Projects: One optional project. I didn't do it and it became a regret of mine.
  - Content:
    - Basics of data wrangling and numerical computation in Python (data structures, Numpy, Scipy sparse matrices, Pandas)
    - Basics of SQL (`SELECT`, `JOIN`, `WHERE`, `GROUPBY`... clauses).
    - Several basic demos of ML algorithms (regression, K-means, PCA).
- **Tips**:
  - Do HW as soon as possible. More difficult to complete hw under time pressure for coding HWs.
  - Do practice questions before exam.

#### 2. Introduction to Analytics Modeling

`iAM` `ISYE6501`

- **DEW**: 5/8/6
- **Format**:
  - HW: Weekly basis. All R markdowns, with a few exceptions:
    - For linear programming, Python's `PuLP` is needed.
    - For discrete event simulation, either Arena or Python's `SimPy` are needed.
  - Exams: 3 exams.
  - Project: 1 project, details released near the end of semester.
  - Content: Learning how to use some ML models in R on data, assess model quality, as well as teaching some basic data science ideas.
- **Tips**:
  - Get used to R and R markdown notebooks, as well as figuring out a suitable workflow, since students have to generate a report file every week.

#### 3. Simulation

`Sim` `ISYE6644`

- **DEW**: 4/8/4
- **Format**:
  - HW: Weekly basis. Multiple choice questions on Canvas.
  - Exams: 3 exams. Allows cheat sheets.
  - Project: 1 project. One can either work on topics supplied by the teaching team, or come up with one.
  - Content:
    - Probabilities, statistics bootcamps.
    - The Arena software,
    - Theories for simulating random number generators and stochastic processes.
- **Tips**:
  - Read Prof. Goldsman's book on probabilities and stats.
  - The tip for having a good score on exams is to compile good cheat sheets.
- **Misc.**:
  - Prof. Goldsman's lecture videos has some funny jokes.

#### 4. Business Fundamentals in Analytics

`BFA` `MGT8803`

- **DEW**: 9/4/3
- **Format**:
  - HW: 2 small ones that accounts for 10% of total grade.
  - Exams: 5 exams for each 5 modules (see below). Allows the use of excel. No cheat sheets.
  - Project: None.
  - Content: 5 modules
    - Financial Accounting
    - Finance
    - Supply Chain
    - Business Strategy
    - Marketing
- **Tips**:
  - The first two modules are extremely packed with info. For people without background related to these fields, all the concepts in these modules can take a fiar while to be digested. Tips for studying for the first two exams
    - Do the self assessment questions repeatedly
    - Get used to the Excel workflow for doing the accounting, finance calculations
    - Check for study cards online, some OMSA alumnis prepared them, e.g. this one on [quizlet](https://quizlet.com/434208661/mgt-8803-accounts-exam-1-flash-cards/).
- **Misc.**:
  - As mentioned above, the first two modules are no-joke - I pulled three all-nighters at the library just to study for these 2 exams.
  - Many people in the OMSA slack channel recommended taking this class during the summer, as one can drop one modules for the final grade calculations.

#### 5. Computational Data Analytics

`CDA` `ISYE6740`

- **DEW**: 7/9/7
- **Format**:
  - This course is basically Machine Learning I. It has mathy parts in it (writing proofs, do hand calculations, implement algorithms, report and explain findings).
  - There are 6 homeworks and 1 final project, no exams.
  - For the final project, our team also worked on a book recommendation system built upon the famous Bookcrossing dataset, using the traditional user-based collaborative filtering (UBCF). The bottleneck we encountered was that the user-item matrix was too large, so we experimented with different interesting approaches to tackle this problem.
- **Misc.**: I enjoyed this course a lot. Lectures are very helpful and clear, and the homeworks are fun to work with.

#### 6. Data Analytics in Business

`DAB` `MGT6203`

- **DEW**: 3/5/3
- **Format**:
  - HW: 3 homeworks in R-markdown format, graded by peer.
  - Exams: 2 midterms, several self-assessments.
  - Project: Team proejct. Our team did some analysis on the Kaggle data set [UFC Dataset](https://www.kaggle.com/datasets/mdabbert/ultimate-ufc-dataset).
  - Tips:
    - Find teams early. The most time will be spent on projects.
- **Misc.**: The technical aspects of this course is covered by iAM, albeit even easier.

#### 7. Data and Visual Analytics

`DVA` `CSE6242`

- **DEW**: 5/6/9
- **Format**:
  - HW: 4 homeworks, graded by autograders.
    - HW2 is a lot of d3.js.
    - HW3 is to play with GCP, AWS, Databricks, Azure, ...
    - HW4 builds a random forest.
  - Exams: No exams.
  - Project: We build a book recommender app; check out our [Github repo](https://github.com/Book-Bender/The-Last-Book-Bender).
  - Tips:
    - Study d3 soon. Learn how to make bar charts, line graphs, choropleth maps. Basic knowledge in DOM structure is beneficial and the autograder is very strict about it.
    - Read through the project specifications carefully, don't miss anything as gradings strictly follows it. E.g., all team members has to record an unlisted Youtube video explaining the poster representations, and I mistakenly assumed that only one video per team is required, so I lost 5 pts for it.
- **Misc.**: I personally think that the major takeaway of this course is the experience to collab with other students, as well as trying to pick up unknown technologies as fast as possible. Although the course touches upon several different technologies, most of the time time is spent on reading through long homework specifications and fighting against the autograder.

#### 8. Higher Dimensional Data Analytics

`HDDA` `ISYE8803`

- **DEW**: 7/10/7
- **Format**:
  - Content:
    - Functional Data Analysis (spline, FPCA)
    - Image Analysis
    - Tensor Data Analysis (Tucker Decomposition, HOSVD)
    - Optimization I (1st+2nd order methods) (Dropped in Summer)
    - Optimization II (Proximal Gradient Descent, ALM+ADMM, Coordinate Descent) (Dropped in Summer)
    - Regularization (Ridge, Lasso, Elastic Net, NNG and Adaptive Lasso, Grouped Lasso)
    - Applications of Regularization (Compressive Sensing, Matrix Completion, RPCA, SSD, RKHS Ridge Kernel Regression)
  - HW and Exams: 2 Exams, 7 Homeworks corresponding to 7 modules (optimization modules dropped in summer).
    - Exams are similar to HWs, but is fun and challenging.
- **Misc.**: **I absolutely loved this course**. Would recommend to anyone in the program that likes math.

#### 9. Network Science

`NS` `CS7280`

- **DEW**: 4/5/5
- **Format**:
  - Content: Network models, core network science notions, community detection, dynamic processes on networks.
  - HW and Exams: 5 HWs (Jupyter notebooks with exercises using `NetworkX` and other related libraries), 14 Quizzes.
- **Misc.**: I don't feel like I learned much from the course; concepts are pretty high-level without clear explanations. The textbook they used is the online textbook by [Barabasi](https://networksciencebook.com/), but I would personally recommend anyone that is interested in network science to look into the book by [Newman](https://global.oup.com/academic/product/networks-9780198805090).

#### 10. Applied Natural Language Processing

`ANLP` `CSE8803`

- **DEW**: 3/6/4
- **Format**:
  - HW: 4 HWs (Jupyter Notebooks with exercises using packages that does text embeddings, or packages in `PyTorch`, `HuggingFace` that does NLP things).
  - Quizzes for each module.
- **Misc.** The contents are cool, allowing us to toy with some cool NLP tools (such as LSTM, BERT).

#### 11. Applied Analytics Practicum

`Prac` `CSE6748`

- **DEW**: 5/8/7
- **Content**:
  - Form a team, and work on a project.
  - Our project is sponsered by [MedTransGo](https://www.medtransgo.com/), where we analyzed their tech update text logs as well as their transaction records (both of which we transformed into time series), to do trend and seasonality detection, correlation analysis, and visualizations.
- **Format**:
  - Deliverables includes Midterm Slidedecks and Final Reports.
  - One also has to watch course videos, accounting for 20% of the grade. For the course videos, the check marks might not indicate a full completion score - **jumping within videos will result in point deductions**.
- **Misc.**: It was in this project that I discovered the crazy power of PowerBI, when I witnessed my teammate using it.

#### 12. Deterministic Optimization

In progress.

#### 13. Deep Learning

In progress.
