---
title: "flusim"
description: "A project on simulating SI processes"
summary: ""
date: 2024-12-01T17:40:15-05:00
lastmod: 2024-12-01T17:40:15-05:00
draft: false
weight: 400
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

{{< inline-svg "outline/brand-github">}} [Github Link](https://github.com/ZebraAlgebra/flusim) {{< inline-svg "outline/file-type-pdf">}} [Report Document](https://drive.google.com/file/d/10dRa2x0HmtnD7IlcfjxcTbAtfH_nD8Qa/view?usp=sharing) {{< inline-svg "outline/brand-python">}} [Python package on TestPyPI](https://test.pypi.org/project/flusim/)

`2023/09-2023/12` `Python` `Simulation` `Markov Processes` `LaTeX`

## Basic Info

This was a project that I worked on in the class Simulation (ISYE-6644) at Georgia Tech's OMSA program.

### The Idea

The project idea was one of those given in a proposed project topics in this course. Roughly speaking, the original topic has the following settings and the corresponding questions posed:

{{< callout context="note" title="Settings" icon="outline/marquee-2" >}}
Consider a population of size 31, and a flu going on in this population. The flu has some properties:
* Day 0, the number of sick students if 1
* An infected person has a probability p=0.02 infecting any healthy person
* An infected person will remain infected for precisely 3 days
* This flu doesn't kill people
{{< /callout >}}

{{< callout context="caution" title="Problem" icon="outline/help-hexagon" >}}
1. Calculate the distribution and expected number of number of people infected at day 1, 2
2. Simulate and find an approximation of the distribution of end-date of flu
{{< /callout >}}

My idea was then to write a Python class (and eventually it became a Python package, though no people use it) that has the following functions:

1. Supports calculations of exact statistics
2. Supports simulations for approximation of statistics
3. Supports basic visualizations of the fluspread process

### My Works

I first formulated a more general version of this problem (where population size, infecting probabilities can be tweaked) mathematically, and designed pseudocodes for exact solvers, simulations for statistics (such as {distributions / expectations / variance} of {number of infected people / end dates}).

The related theory I used for designing the exact solver was that of Markov chain[^1], where some of the statistics can be done via such general methods - for example, expectations, variance of end dates are analyzed via *first step analysis* techniques. 

[^1]: This was a fun problem to work with from a mathematical viewpoint, but it was later that I learned that such model is a type of [**SI model**](https://en.wikipedia.org/wiki/Compartmental_models_in_epidemiology) (without the "R").

### Some Screenshots

{{< tabs "screenshots" >}}
{{< tab "Package" >}}
![flusim package screenshot](images/about/flusim-sc.png)
{{< /tab >}}
{{< tab "Report" >}}
Fragments of final report (page 1, 5, 8, 11)
![Fragments of written report.](images/about/flusim-r.gif)
{{< /tab >}}
{{< /tabs >}}

## Final Thoughts

It was pretty cool seeing the things I derived with the theory of Markov chains matching the simulation results, a type of "mathematical joy" I would say.

{{< card-grid >}}
{{< link-card title="Back to Projects Page" href="/about/projects/" >}}
{{< link-card title="Back to Resume" href="/about/resume/" >}}
{{< /card-grid >}}
