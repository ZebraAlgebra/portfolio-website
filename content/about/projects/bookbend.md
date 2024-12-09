---
title: "The Last Book Bender"
description: "A project on building a book recommender"
summary: ""
date: 2024-12-03T17:40:15-05:00
lastmod: 2024-12-03T17:40:15-05:00
draft: false
weight: 200
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

{{< inline-svg "outline/brand-github">}} [Github Link](https://github.com/Book-Bender/The-Last-Book-Bender)

`2024/01-04/2024` `Python` `BERT` `Recommendation Systems` `ReactJS` `Flask`

## Basic Info

This was a project that I worked on in the class Data and Visual Analytics (CSE-6242) at Georgia Tech's OMSA program, parterned with teamates [Ryan Tsedevsuren](https://www.linkedin.com/in/ryan-tsedevsuren/), [Tyler David](https://www.linkedin.com/in/tyler-david1999/), [Terrance Patric Lenaghan](https://www.linkedin.com/in/tplenaghan/), [Timothy Zhang](https://www.linkedin.com/in/timothy-zhang/), [Swathi Naik](https://www.linkedin.com/in/swathimnaik/).

### The Idea

We wanted to create a book webapp that allows interactive query and recommendation visualizations, built on top of the datasets [`goodbooks-10k`](https://github.com/zygmuntz/goodbooks-10k) and [Project Gutenberg](https://www.gutenberg.org/).

We want to implement both the CF (collaborative filtering) and CBF (content-based filtering) functionalities; an brief overview of what these do can be found in this [Wikipedia link](https://en.wikipedia.org/wiki/Recommender_system#Approaches), or this textbook[^1]. We intended the user to interact with the app in the following ways:

1. In the first way, the users may enter a prompt, indicating their preferences, and our CBF backend API endpoint will search for top books that matches this response utilizing the [`bert-base-uncased`](https://huggingface.co/google-bert/bert-base-uncased) model.
2. In the second way, the users may have an anonymized view of other users, and if their is a match in preferences, our CF backend API endpoint will find the top books that the users might also like. We tried to look for existing implementations, such as the [`surprise`](https://github.com/NicolasHug/Surprise) library. However we found that some sparse implementations and fine-tweaks might be needed to fit our needs, so I decided to implment it myself.
3. In both ways, the API endpoints are implemented in [`flask`](https://github.com/pallets/flask).
4. In both ways, we visualize the books as force graphs, where each book is a node. The users can drag around, zoom in/out on the force graphs, and right click to expand a node's most similar nodes. Here we implemented the UI and force graphs functionalities via [`material-ui`](https://github.com/mui/material-ui), [`react-force-graph`](https://github.com/vasturiano/react-force-graph) React libraries.

{{< inline-svg "outline/backhoe" >}} **To appear: System Design Diagram**

[^1]: Aggarwal, Charu C. _Recommender systems_. Vol. 1. Cham: Springer International Publishing, 2016.

### My contributions

My contributions are summarized in the following table:

| Components               | Implementation                                                         | Role                                                                               |
| :----------------------- | :--------------------------------------------------------------------- | :--------------------------------------------------------------------------------- |
| Frontend - UI            | [`material-ui`](https://github.com/mui/material-ui)                    | Main implementation                                                                |
| Frontend - Visualization | [`react-force-graph`](https://github.com/vasturiano/react-force-graph) | Main implementation                                                                |
| Backend                  | [`flask`](https://github.com/pallets/flask)                            | Exposed CF Functionality as an API endpoint                                        |
| Modeling - CF            | From scratch                                                           | Implemented CF from scratch, and tested different similarity metrics via 9-fold CV |

### Animated Screenshots

The final app has the following look (animated GIF generated from our [unlisted YouTube Video Demo](https://www.youtube.com/watch?v=-kzubcvd4as), produced with CLI tools `yt-dlp`, `ffmpeg`, `magick`):

![Demo of Webapp](images/about/bookbender.gif)

## Issues and Rooms for Improvements

I thought the idea of project was pretty cool, but I will talk about some improvement directions and related takeaways on my side (some of which are things that I wished I had more time to spent working on on my part):

- **{{< inline-svg "outline/rocket" >}} Deployment Issues**: We tried to find free solutions for deploying this webapp online, but the final webapp was pretty large, so we decided to keep it as an app that can be built locally. The main reason was that the backend functionality for CBF uses the entire [`bert-base-uncased`](https://huggingface.co/google-bert/bert-base-uncased) model, which was about 0.5GB in size (without accounting for the size of other Python libraries needed). A possible direction for improvement is to use distilled version of it (either [`distilbert-base-uncased`](https://huggingface.co/distilbert/distilbert-base-uncased) or [`TinyBERT_General_4L_312D`](https://huggingface.co/huawei-noah/TinyBERT_General_4L_312D)).

- {{< inline-svg "outline/users" >}} **Exploration Issues**: The exploration ability of the force graph is actually pretty limited - each time we generate top 5 recommendations, but we often ended up in a complete graph, and each node expands to nodes that we have seen before, making the exploration process stagnant. We do not know if this is an issue in our modeling process (whether the CBF or the CF part), our data (where we have very strong nodes dominating the whole graph).

- {{< inline-svg "outline/users" >}} **UI/UX Issues**: The view for existing users is extremely inconvenient - I implemented in a way that one can only click alone one direction to look at one book at a time. This is one part that I wanted to improve, but I was not very adept with the MUI library at that time.

- {{< inline-svg "outline/device-tablet-minus" >}} **RWD Design**: I didn't have time finishing the webapp design for adaptability for devices of various size, which is a crucial aspect of modern webapp development, although breakpoints for media queries were used.

## Final Thoughts

I learned a lot from this project:
1. I used to have some "have watched some Udemy React course" React skill, and vague experience with other frontend development stuffs, but this project really pushed me to put these into works.
2. This is my first time reading Flask backend codes, connecting frontend apps to it, as well as designing some additional endpoints. I used to have a vague idea on how maybe Python can be used to do such things, but working with teammates that have backend skills enabled me to see how this *actually works*.
3. This is my first time learning about the BERT model. I made up my mind at that time to learn about this tool and possibly use it in the future when encountering analytics tasks involving NLP components.

Most importantly, this is my first time trying to build an end-to-end pseudo-complete data product with a team. It might be a weird to say this, but I always find it exciting and happy to see when datas "doing things". 

{{< card-grid >}}
{{< link-card title="Back to Projects Page" href="/about/projects/" >}}
{{< link-card title="Back to Resume" href="/about/resume/" >}}
{{< /card-grid >}}
