---
title: "Applied Analytics Practicum"
description: "My practicum project"
summary: ""
date: 2024-12-02T17:40:15-05:00
lastmod: 2024-12-02T17:40:15-05:00
draft: false
weight: 100
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

`2024/09-2024/12` `Python` `PowerBI` `Time Series Analysis`

## Basic Info

This is the practicum project I did in OMSA, partnered with [Ziyang Guo](https://www.linkedin.com/in/yangguoo/), supervised by [MedTrans Go](https://www.medtransgo.com/).

### The Task

Our task is to analyze tech update text logs (these are given in the form of websites and google docs), as well as request records (in the form of a `csv` file with a data dictionary), quantifying impact of tech udpates on sales, as well as doing seasonality, trend detections on sales.

### My contributions

| Components               | Implementation                                                         | Role                                                                               |
| :----------------------- | :--------------------------------------------------------------------- | :--------------------------------------------------------------------------------- |
| Text Extraction | [`bs4`](https://beautiful-soup-4.readthedocs.io/en/latest/), [`re`](https://docs.python.org/3/library/re.html) | Designed scripts for extraction and tabulation of relevant data from webpage and Google docs |
| Data Wrangling | [`polars`](https://pola.rs/)                    | Aggregate, filter, and ran basic diagnosis on data |
| Dashboard | [PowerBI](https://www.microsoft.com/en-us/power-platform/products/power-bi), [`matplotlib`](https://matplotlib.org/) | Prepared data for Ziyang to build the dashboard, generated other preliminary visualizations with `matplotlib` |
| Descriptive Analysis | [PowerBI](https://www.microsoft.com/en-us/power-platform/products/power-bi)| None |
| Modeling            | [statsmodels.tsa](https://www.statsmodels.org/stable/tsa.html) | Use ACF, PACF, CCF functions and KPSS tests for trend, seasonality detection, correlation analysis of time series|
| Reporting | MS PPT, {{< math >}}$\LaTeX${{< /math >}} | Collaborated on a slidedeck for progress report; Combined and typesetted teammates inputs into a {{< math >}}$\LaTeX${{< /math >}} final report|

### Some Screenshots

{{< tabs "screenshots" >}}
{{< tab "Slidedeck" >}}
Fragments of midterm slidedeck (with info censored due to NDA)
![Slidedeck](images/about/prac-m.gif)
{{< /tab >}}
{{< tab "Report" >}}
Fragments of final report (with info censored due to NDA)
![Report](images/about/prac-f.gif)
{{< /tab >}}
{{< /tabs >}}
## Final Comments

I feel like this project is the closest to an end-to-end data analytics project in this program. The experience working directly with and under other analytics professionals is also valuable. The first time I saw PowerBI in action absolutely amazed me (sadly it does not natively supports Linux).

Although learning about nerdy time series models and statistical knowledges along the way of this project are also very fun to me, I think one of the most exciting aspect of this project for me is that the result of this project can directly help people from the corporation - such as insights in to which types of tech updates have been the most impactful, or the characteristics of the requests data. 

{{< card-grid >}}
{{< link-card title="Back to Projects Page" href="/about/projects/" >}}
{{< link-card title="Back to Resume" href="/about/resume/" >}}
{{< /card-grid >}}
