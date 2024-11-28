---
title: "Ellipsoid Method"
description: ""
summary: ""
date: 2024-11-21T01:58:02-05:00
lastmod: 2024-11-21T01:58:02-05:00
draft: false
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

In this article, I will give a brief guide on what the _ellipsoid method_ is. A good reference would be the note by Sébastien Bubeck [^1].

[^1]: Bubeck, Sébastien. _"Convex optimization: Algorithms and complexity."_ Foundations and Trends® in Machine Learning 8.3-4 (2015): 231-357.

I will first give a high-level breakdown on why this algorithm works, then establish each separate part of this algorithm. Mathematical proofs are collected in the last part.

Another optimization algorithm that is seldomly used in practice, but conceptually closely-related is the _center of gravity_ method. This will be explained in another article.

## 1. Setting the Stage

### 1.1. Assumptions and Notations

**Optimization Problem**. Minimize a convex function {{< math >}}$f(x)${{< /math >}} defined over a convex body {{< math >}}$\mathcal{X}\subset{\mathbb{R}}^m${{< /math >}}.

General results on convex analysis guarantees that {{< math >}}$f${{< /math >}} attains minimum on some {{< math >}}$x^\ast\in\mathcal{X}${{< /math >}}; let us also write the optimal value as {{< math >}}$f^\ast${{< /math >}}.

**Assumptions**. For {{< math >}}$f,\mathcal{X}${{< /math >}}, we make the assumptions:

1. **Value Bound**. {{< math >}}$\|f\|_{\mathcal{X},\infty}:=\{|f(x)|:x\in \mathcal{X}\}\leq B${{< /math >}} for some {{< math >}}$B>0${{< /math >}}.
2. **Volume Bound**. {{< math >}}$B(z_1;r)\subset\mathcal{X}\subset B(z_2;R)${{< /math >}} for some {{< math >}}$x_1,x_2\in\mathbb{R}^m${{< /math >}}, {{< math >}}$0<r<R${{< /math >}}; here {{< math >}}$B(z;d)${{< /math >}} is the open ball centered at {{< math >}}$x${{< /math >}} with radius {{< math >}}$d${{< /math >}}.

**Available Oracles**. We assume the following 0th and 1st-order oracles available to us:

1. **Separation Oracle**. Given {{< math >}}$x\notin\mathcal{X}${{< /math >}}, we can ask for a direction {{< math >}}$O\neq w\in\mathbb{R}^{m}${{< /math >}} with {{< math >}}$\mathcal{X}\subset E^-_{w,w^Tx}${{< /math >}}, where {{< math >}}$E^{-}_{a,b}${{< /math >}} is the half space {{< math >}}$\{x:a^Tx\leq b\}${{< /math >}}.
2. **Subgradient Oracle**. Given {{< math >}}$x\in\mathcal{X}${{< /math >}}, we can ask for a direction {{< math >}}$w\in\partial f(x)${{< /math >}}.

### 1.2. Utilizing Volume and Value Bounds via Shrinking

To simplify notation, given {{< math >}}$X,Y\subset\mathbb{R}^m,Z\subset\mathbb{R}${{< /math >}}, we can formulate a set

{{< math class="text-center">}}

$$
I(X,Y;Z):=\{(1-z)x+zy:(x,y,z)\in X\times Y\times Z\}
$$

{{< /math >}}

so for instance, setting {{< math >}}$Z=[0,1]${{< /math >}} gives convex combinations of elements between {{< math >}}$X,Y${{< /math >}}.

Intuitively, points close to {{< math >}}$x^\ast${{< /math >}} shouldn't be too bad. Although we do not know {{< math >}}$x^\ast${{< /math >}}, it still makes sense to consider the following construction: Given {{< math >}}$\varepsilon\in[0,1]${{< /math >}}, define the set:

{{< math class="text-center">}}$$\mathcal{X}_{\varepsilon}=I(x^\ast,X;\varepsilon)$${{< /math >}}

Here we do not make clear distinctions between one-element sets and elements. On this set, we have the function bounds and volume bounds on {{< math class="text-center">}}$\mathcal{X}_{\varepsilon}${{< /math >}}:

{{< math class="text-center">}}$$\sup f(\mathcal{X}_\varepsilon)\leq f^\ast+2\varepsilon B$${{< /math >}}

{{< math class="text-center">}}$$\varepsilon^m\operatorname{vol}(B(O;r))\subset \operatorname{vol}(\mathcal{X}_\varepsilon)\leq \varepsilon^m\operatorname{vol}(B(O;R))$${{< /math >}}

by utilizing our assumptions on convexity, volume and value bounds. In this sense, we have the following general idea:

> If we are able to solve for an optimal point in a major portion of the feasibility region, this point would in fact be close to the true optimal solution.

We formalize this idea and give an abstract proof of why the ellipsoid method works.

### 1.3. General Proof of Convergence

The ellipsoid method is an iterative method. In each step, it gains total control of a part of the feasibility region, by using ellipsoids as a proxy, through halving along subgradients or separating hyperplanes.

Suppose at time {{< math >}}$t${{< /math >}}, the remaining uncontrolled region is written as {{< math >}}$\mathcal{S}_t\subset\mathcal{X}${{< /math >}}. This gives us a descending sequence of subsets:

{{< math class="text-center">}}$$\mathcal{X}=\mathcal{S}_1\supset\mathcal{S}_2\supset\mathcal{S}_3\supset\dotsc$${{< /math >}}

As an old adage goes:

> To control an onion, all you have to do is to control its peels.

we mathematically express {{< math >}}$\mathcal{S}_1\setminus\mathcal{S}_{t+1}=\coprod_{i=1}^tP_t${{< /math >}}, where {{< math >}}$P_t:=\mathcal{S}_{t+1}\setminus\mathcal{S}_t${{< /math >}} are the peels, and formulate strategies to control {{< math >}}$P_t${{< /math >}}.

Now for each set {{< math >}}$P_t${{< /math >}}, say we have a point {{< math >}}$c_t\in\mathbb{R}^m${{< /math >}} with either {{< math >}}$P_t=\emptyset${{< /math >}}, or {{< math >}}$c_t\in \mathcal{X}${{< /math >}} with {{< math >}}$f(c_t)\leq \inf f(P_t)${{< /math >}}, then by taking {{< math >}}$x_t=\operatorname{argmin}f(\{c_i\}_{i=1}^t)${{< /math >}}, and assuming {{< math >}}$\operatorname{vol}(\mathcal{S}_t)\to 0${{< /math >}}, we in fact have {{< math >}}$f(x_t)\to f^\ast${{< /math >}}. For a proof, note that for any {{< math >}}$\varepsilon>0${{< /math >}}, the volume bounds on {{< math >}}$\mathcal{X}_\varepsilon${{< /math >}} shows that {{< math >}}$\mathcal{S}_t${{< /math >}} cannot contain {{< math >}}$\mathcal{X}_\varepsilon${{< /math >}} for large enough {{< math >}}$t${{< /math >}}, while we have:

{{< math class="text-center">}}$$\begin{align*}
f(x_t)&\leq \inf f(\{c_i\}_{i=1}^t)\leq \inf f(\mathcal{S}_1\smallsetminus\mathcal{S}_{t+1})\\
&\leq \inf f(X_\varepsilon\smallsetminus\mathcal{S}_{t+1})\leq f^\ast+2B\varepsilon
\end{align*}$${{< /math >}}

The following diagram might be useful for navigating the definitions and symbols (coutesy to [draw.io](https://www.drawio.com/))

![Schematic depiction of the abstract idea of onionification.](images/ellipse/onion.jpg)

In optimization, we are also interested in the question of the speed of convergence. By using the same idea for estimation, we see that it depends on {{< math >}}$\operatorname{vol}(\mathcal{S}_t)${{< /math >}}. In ellipsoid methods - as one can guess it - these are given manipulation with ellipsoids; in center of gravity methods, these are given by other means.

### 1.4. Using Ellipsoids and Subgradients

It is now (finally 😅) the time to introduce the ellipsoid algorithm. The steps are as follows:

- **Initiallize**: Ellipsoid {{< math >}}$\mathcal{E}_0=B(z_1;R)${{< /math >}}, {{< math >}}$\mathcal{S}_1=\mathcal{X}${{< /math >}}, {{< math >}}$c_1=x_1=z_1${{< /math >}}, {{< math >}}$t=1${{< /math >}}
- **Halving**:
  - If {{< math >}}$c_t\notin \mathcal{X}${{< /math >}}, call separation oracle for a nonzero direction {{< math >}}$w_t${{< /math >}}, so that {{< math >}}$\mathcal{X}\subset E^-_{w_t,w_t^Tc_t}${{< /math >}}
  - Else call subgradient oracle for a direction {{< math >}}$w_t\in\partial f(c_t)${{< /math >}}. If {{< math >}}$w_t=O${{< /math >}}, optimality condition reached, terminate. Otherwise continue.
- **Update**: Update {{< math >}}$\mathcal{E}_{t+1}${{< /math >}} via the explicit formulas in the next section, to have the properties:
  {{< math class="text-center">}}$$E^-_{w_t,w_t^Tc_t}\cap \mathcal{E}_{t}\subset \mathcal{E}_{t+1}$${{< /math >}}
  {{< math class="text-center">}}$$\operatorname{vol}(\mathcal{E}_{t+1})\leq \exp(-1/2m)\operatorname{vol}(\mathcal{E}_{t})$${{< /math >}}
  and update:
  - {{< math >}}$c_{t+1}\to${{< /math >}} to be the new center of this ellipsoid.
  - {{< math >}}$x_{t+1}\to${{< /math >}} the argmin of {{< math >}}$\{f(x_t),f(c_{t+1})\}${{< /math >}} if {{< math >}}$c_{t+1}\in\mathcal{X}${{< /math >}}; else continue.
  - {{< math >}}$\mathcal{S}_{t+1}\to\mathcal{E}_{t+1}\cap \mathcal{X}${{< /math >}}.
  - {{< math >}}$t\to t+1${{< /math >}}.

Note that the sets {{< math >}}$\mathcal{S}_t${{< /math >}} and points {{< math >}}$c_t,x_t${{< /math >}} then satisfies the settings we previously introduced that will lead to convergence. With a bit of algebra, one has the following:

{{< callout context="caution" title="Ellipsoid Method: Feasibility and Convergence" icon="outline/note" >}}
For {{< math >}}$t\geq 2m^2\log(Rr^{-1})${{< /math >}}, we have {{< math >}}$x_t\in\mathcal{X}${{< /math >}}, with:
{{< math class="text-center">}}$$f(x_t)-f^\ast\leq 2BRr^{-1}\exp(-t/2m^2)$${{< /math >}}
{{< /callout >}}

A bit of interpretation on this result, which would illustrate some cool characteristics of this algorithm:

1. The _analytical complexity_ (that is, the number of calls to the oracles needed) to guarantee an accuracy to {{< math >}}$O(\varepsilon)${{< /math >}} is {{< math >}}$m^2\log(Rr^{-1}\varepsilon^{-1})${{< /math >}}, from a black-box optimization perspective.
2. In such sense, it is a _dimension-dependent_ algorithm - as dimension grows, the calls needed grows.
3. As one can see later, the cost update are just some matrix-vector multiplications, as opposed to center-of-gravity which although have a better analytical complexity (which is {{< math >}}$\varepsilon${{< /math >}}), but each time step requires the computation of a nontrivial integral, in which in the most easy cases exact solvers still needs exponential computation time.

## 2. Ellipsoidal Shenanigans

Now let us look at some technical tools and results that allow us to work with ellipsoids, tying together the lose ends introduced in the algorithm above.

It is just a brief note on how the math is done, leaving out much of the book-keeping and formula derivations. For even more casual readers, you have already understand what ellipsoid method does🎉!

### 2.1. Representation of an Ellipsoid

An ellipsoid {{< math >}}$\mathcal{E}\subset\mathbb{R}^m${{< /math >}} is an affine image of {{< math >}}$B(O;1)${{< /math >}}. It can be represented as:

{{< math class=text-center >}}

$$
\mathcal{E}=\mathcal{E}(c,H):=\{x\in\mathbb{R}^m:(x-c)^TH^{-1}(x-c)\leq 1\}
$$

{{< /math >}}

where {{< math >}}$H${{< /math >}} is SPD (symmetric positive definite) (assuming it having positive volume), admitting a decomposition {{< math >}}$H=A^TA${{< /math >}}; such {{< math >}}$A${{< /math >}} then describes {{< math >}}$\mathcal{E}${{< /math >}} as {{< math >}}$c+AB(O;1)${{< /math >}}, hence an ellipsoid.

### 2.2. "Ellipsoiding" Halved Ellipsoids

Here is a fun problem in geometry:

{{< callout  title="Question" icon="outline/question-mark" >}}
Given an ellipsoid with positive volume {{< math >}}$\mathcal{E}(c_0,H_0)${{< /math >}}, a direction {{< math >}}$O\neq w\in\mathbb{R}^{m}${{< /math >}}, how small an ellipsoid (in terms of volume) {{< math >}}$\mathcal{E}(c,H)${{< /math >}} can we find so that it encloses the halved ellipsoid {{< math >}}$\mathcal{E}(c_0,H_0)\cap E^-_{w,w^Tc_0}${{< /math >}}?
{{< /callout >}}

The case {{< math >}}$m=1${{< /math >}} is trivial, so we assume {{< math >}}$m>1${{< /math >}}.

It would be illustrative to work out the case where {{< math >}}$c_0=O,H=\mathbf{I}_m${{< /math >}}, and {{< math >}}$\|w\|=1${{< /math >}}, then map it back using {{< math >}}$x\mapsto \sqrt{H_0}x + c_0${{< /math >}}. We want {{< math >}}$\mathbb{S}^{m-1}\cap\{w\}^\perp${{< /math >}} and {{< math >}}$\{-w\}${{< /math >}} lie in {{< math >}}$\partial\mathcal{E}(c,H)${{< /math >}}, so we define:

{{< math class="text-center">}}

$$
c=-tw,\;H^{-1}=aww^T+b(\mathbf{I}_m-ww^T)
$$

{{< /math >}}

with {{< math >}}$t\in[0,1/2)${{< /math >}}; note that {{< math >}}$w^TH^{-1}w=a${{< /math >}}, {{< math >}}$v^TH^{-1}v=b${{< /math >}} for {{< math >}}$v\in \{w\}^\perp\cap\mathbb{S}^{m-1}${{< /math >}}. By this requirement, we formulate the optimization problem:

{{< math class="text-center">}}

$$
\text{Maximize: }\frac{\operatorname{vol}(B(0;1))^2}{\operatorname{vol}(\mathcal{E}(c,H))^2}=ab^{m-1}
$$

{{< /math >}}

{{< math class="text-center">}}

$$
\text{subject to: }
\begin{cases}
t\in[0,1/2)\\
(t-1)^2a=1\\
b+t^2a=1
\end{cases}
$$

{{< /math >}}

After expressing {{< math >}}$a,b${{< /math >}} via {{< math >}}$t${{< /math >}}, we have by calculus that the optimal point is {{< math >}}$t=(m+1)^{-1}${{< /math >}} with value:

{{< math class="text-center">}}

$$
(1+m^{-1})^{2}(1-m^{-2})^{m-1}\geq\exp(m^{-1})
$$

{{< /math >}}

After taking account the rescaling of {{< math >}}$w${{< /math >}} and the remapping of points {{< math >}}$x\mapsto\sqrt{H_0}x+c_0${{< /math >}}, we get:

{{< callout context="caution" title="Ellipsoid Update Formula" icon="outline/note" >}}
For {{< math >}}$m\geq 2${{< /math >}}, we get:

{{< math class="text-center">}}

$$
\begin{cases}
&\mathcal{E}(c_0,H_0)\cap E^-_{w,w^Tc_0}\subset \mathcal{E}(c,H)\\
&\operatorname{vol}(\mathcal{E}(c,H))\leq e^{-1/2m}\operatorname{vol}(\mathcal{E}(c_0,H_0))
\end{cases}
$$

{{< /math >}}
where:

{{< math class="text-center">}}

$$
\begin{cases}
&c=c_0-\frac{1}{n+1}\frac{H_0w}{\sqrt{w^TH_0w}}\\
&H=\frac{n^2}{n^2-1}\left(H_0-\frac{2}{n+1}\frac{H_0ww^TH_0}{w^TH_0w}\right)
\end{cases}
$$

{{< /math >}}
{{< /callout >}}
