---
title: "Center of Gravity Method"
description: ""
summary: ""
date: 2024-11-28T12:37:23-05:00
lastmod: 2024-11-28T12:37:23-05:00
draft: false
weight: 220
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

In this article, I will give a brief guide on what the _center of gravity method_ (COG) is. Again, a good reference would be the note by Sébastien Bubeck[^1].

[^1]: Bubeck, Sébastien. _"Convex optimization: Algorithms and complexity."_ Foundations and Trends® in Machine Learning 8.3-4 (2015): 231-357.

We will use the same settings and borrow parts of our exposition from the ellipsoid method[^2], where the convergence analysis follows along the same line as in that note's [section 1.3](../ellipse//#13-general-proof-of-convergence).

[^2]: [Ellipsoid Method](../ellipse), on this site.

## 1. Setting the Stage

### 1.1. First Comparison with the Ellipsoid Algorithm

A high level description of the ellipsoid algorithm is that total control of a part of the feasibility region - the "onion peels" - are gained within each iteration via slicing along suitable directions (either it being a direction for a separating hyperplanes, or a direction given by subgradients), and by volume and shrinking arguments, as the uncontrolled feasibility region shrinks, the optimal value on regions on the peels, would not be too far from that from the uncontrolled region.

The "ellipsoidal" parts comes in the part where we want to gain control to a next peel, which uses ellipsoids as proxies. In center of gravity method, as one can guess it - we use center of gravities.

### 1.2. The Algorithm

Let us use again {{< math >}}$\mathcal{P}_t,\mathcal{S}_t${{< /math >}} to denote the "peel" and the "remaining onion" at time {{< math >}}$t${{< /math >}}.

- **Initiallize**: {{< math >}}$\mathcal{S}_1=\mathcal{X}${{< /math >}}, {{< math >}}$t=1${{< /math >}}, {{< math >}}$x_1${{< /math >}} to be any point in {{< math >}}$\mathcal{X}${{< /math >}}.
- **Halving**:

  - Call COG oracle (here we think of it as a zeroth order oracle) to obtain the COG:
    {{< math class="text-center">}}$$c_{t+1}=\frac{1}{\operatorname{vol}(\mathcal{S}_t)}\int_{x\in\mathcal{S}_t}x\mathrm{d}x$${{< /math >}}

  - Call subgradient oracle obtain {{< math >}}$w_t\in\partial f(c_t)${{< /math >}}. If {{< math >}}$w_t=O${{< /math >}}, optimality condition reached, terminate. Otherwise continue.

- **Update**:
  - {{< math >}}$\mathcal{S}_{t+1}\to E^-_{w_t,w_t^Tc_t}\cap\mathcal{S}_t${{< /math >}}; which has the property:
    {{< math class="text-center">}}$$\operatorname{vol}(\mathcal{S}_{t+1})\leq(1-e^{-1})\operatorname{vol}(\mathcal{S}_{t})$${{< /math >}}
  - {{< math >}}$x_{t+1}\to${{< /math >}} the argmin of {{< math >}}$\{f(x_t),f(c_{t+1})\}${{< /math >}}.
  - {{< math >}}$t\to t+1${{< /math >}}

One has the following:

{{< callout context="caution" title="COG Method: Convergence" icon="outline/note" >}}
We have the following bound:
{{< math class="text-center">}}$$f(x_t)-f^\ast\leq 2B(1-e^{-1})^{t/n}$${{< /math >}}
{{< /callout >}}

Some remarks:

- The step "Compute center of gravity" is a highly nontrivial step in general if one wants exact solutions (e.g., think of the problem of computing the COG of a simplex with {{< math >}}$O(t)${{< /math >}} vertices). In such sense, this algorithm is more of theoretical importance then of practical use.
- The volume inequality during the passage from {{< math >}}$\mathcal{S}_{t}${{< /math >}} to {{< math >}}$\mathcal{S}_{t+1}${{< /math >}} will be shown below - it is related to the so-called **Grünbaum Inequality**, which can be proved by also another famous inequality called **Brunn-Minkowski Ineuqality**.
- The _analytical complexity_ to guarantee an accuracy of {{< math >}}$O(\varepsilon)${{< /math >}} is {{< math >}}$O(m\log(2B\varepsilon^{-1}))${{< /math >}}. Compared to ellipsoid method's {{< math >}}$O(m^2\log(Rr^{-1}\varepsilon^{-1}))${{< /math >}}, both having _linear rate_ of convergence, it is less sensitive to the underlying dimension {{< math >}}$m${{< /math >}}.

## 2. Math of COG

{{< inline-svg "outline/barrier-block" >}} Under Construction!

**Goal**. Prove Grünbaum's inequality

**Tentative outline**.

- 2.1. Brunn-Minkowski inequality
- 2.2. Grünbaum inequality
