---
title: "'Now' Page"
description: "A now page"
summary: "A now page"
date: 2024-11-20T17:49:31-05:00
lastmod: 2024-11-20T17:49:31-05:00
draft: false
weight: 400
pinned: false
homepage: false
seo:
  title: "" # custom title (optional)
  description: "Now page" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

{{< callout context="tip" title="Last updated on 2025-01-09" icon="outline/progress-check" >}}{{< /callout >}}

This is a ["Now" Page](https://nownownow.com/about).

## What I'm Learning

- {{< inline-svg "outline/math">}} **Math**: Convex Optimization
- {{< inline-svg "outline/chart-bar-popular">}} **Visualization Tools**: Visx, PowerBI, Looker

## What I'm Reading

- {{< inline-svg "outline/bible">}} **Daily Devotional**. *Love On: A Study Through 1 John*, a study plan on YouVersion.
- {{< inline-svg "outline/book">}} **Books**.
    - **Spiritual**. *Knowing God*, by J. I. Packer.
    - **Technical**. *Lectures on Convex Optimization*, by Yurii Nesterov.
    - **Technical**. *Designing Data-Intensive Applications: The Big Ideas Behind Reliable, Scalable, and Maintainable Systems*, by Martin Kleppmann.

## What I'm Working On

- {{< inline-svg "outline/briefcase-2">}} **Job**. Applying for jobs! As well as refining resume.
- {{< inline-svg "outline/code">}} **Project Building**. Building a project on the [College Scorecard Open Data](https://collegescorecard.ed.gov/data/). The plan (current progress: database setup completed):
    - The project would consist of two parts -
        1. Build a PostgresSQL database from the raw data files, document it, using this site.
        2. Build interactive visualizations from the files, using a subset of the data.
    - Technology:
        1. The visualization would consist of a webapp, using [`visx`](https://airbnb.io/visx/) + [`DaisyUI`](https://daisyui.com/) + [`NextJS`](https://nextjs.org/) + [`ReactJS`](https://react.dev/), and deploy on [Vercel](https://vercel.com/), with PostgresSQL database setup on [`Neon`](https://neon.tech) to utilize NextJS' serverside rendering, data fetching.
        2. Use `polars` for data wranggling.
- {{< inline-svg "outline/writing">}} **Website Content Generation**. Plan to add:
    - Math: Commonly-used Function classes (notions on convexity, self-concordance, PL(Polyak-Łojasiewicz)), Interior point methods, Gradient Methods, Lower Bounds.
    - Blog: Math journey.

## What I'm Watching

On [MyAnimeList](https://myanimelist.net/animelist/Cabbage_Cat?status=1).
