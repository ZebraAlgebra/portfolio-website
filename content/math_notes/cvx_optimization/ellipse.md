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

Another optimization that is seldomly used in practice, but conceptually closely-related is the _center of gravity_ method. This will be explained in another article.

## 0. Assumptions and Settings

**Optimization Problem**. Minimize a convex function {{< math >}}$f(x)${{< /math >}} defined over a convex body {{< math >}}$\mathcal{X}\subset{\mathbb{R}}^m${{< /math >}}.

General results on convex analysis guarantees that {{< math >}}$f${{< /math >}} attains minimum on some {{< math >}}$x^\ast\in\mathcal{X}${{< /math >}}.

**Assumptions**. For {{< math >}}$f,\mathcal{X}${{< /math >}}, we make the assumptions:

1. **Value Bound**. {{< math >}}$\|f\|_{\mathcal{X},\infty}:=\{|f(x)|:x\in \mathcal{X}\}\leq B${{< /math >}} for some {{< math >}}$B>0${{< /math >}}.
2. **Volume Bound**. {{< math >}}$B(x_1;r)\subset\mathcal{X}\subset B(x_2;R)${{< /math >}} for some {{< math >}}$x_1,x_2\in\mathbb{R}^m${{< /math >}}, {{< math >}}$0<r<R${{< /math >}}; here {{< math >}}$B(x;d)${{< /math >}} is the open ball centered at {{< math >}}$x${{< /math >}} with radius {{< math >}}$d${{< /math >}}.

**Available Oracles**. We assume the following 0th and 1st-order oracles available to us:

1. **Separation Oracle**. Given {{< math >}}$x\notin\mathcal{X}${{< /math >}}, we can ask for a direction {{< math >}}$O\neq w\in\mathbb{R}^{m}${{< /math >}} with {{< math >}}$\mathcal{X}\subset E^-_{w,w^Tx}${{< /math >}}, where {{< math >}}$E^{-}_{a,b}${{< /math >}} is the half space {{< math >}}$\{x:a^Tx\leq b\}${{< /math >}}.
2. **Subgradient Oracle**. Given {{< math >}}$x\in\mathcal{X}${{< /math >}}, we can ask for a direction {{< math >}}$w\in\partial f(x)${{< /math >}}.

## 1. Ellipsoidal Shenanigans

### 1.1. Representation of an Ellipsoid

An ellipsoid {{< math >}}$\mathcal{E}\subset\mathbb{R}^m${{< /math >}} is an affine image of {{< math >}}$B(O;1)${{< /math >}}. It can be represented as:

{{< math class=text-center >}}

$$
\mathcal{E}=\mathcal{E}(c,H):=\{x\in\mathbb{R}^m:(x-c)^TH^{-1}(x-c)\leq 1\}
$$

{{< /math >}}

where {{< math >}}$H${{< /math >}} is SPD (symmetric positive definite) (assuming it having positive volume), admitting a decomposition {{< math >}}$H=A^TA${{< /math >}}; such {{< math >}}$A${{< /math >}} then describes {{< math >}}$\mathcal{E}${{< /math >}} as {{< math >}}$c+AB(O;1)${{< /math >}}, hence an ellipsoid.

### 1.2. "Ellipsoiding" Halved Ellipsoids

Here is a fun problem in geometry:

{{< callout context="none" title="Question" icon="outline/question-mark" >}}
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

{{< callout context="note" title="Lemma 1" icon="outline/note" >}}
For {{< math >}}$m\geq 2${{< /math >}}, we get:

{{< math >}}

$$
\begin{cases}
&\mathcal{E}(c_0,H_0)\cap E^-_{w,w^Tc_0}\subset \mathcal{E}(c,H)\\
&\operatorname{vol}(\mathcal{E}(c,H))\leq e^{-1/2n}\operatorname{vol}(\mathcal{E}(c_0,H_0))
\end{cases}
$$

{{< /math >}}
where:

{{< math >}}

$$
\begin{cases}
&c=c_0-\frac{1}{n+1}\frac{H_0w}{\sqrt{w^TH_0w}}\\
&H=\frac{n^2}{n^2-1}\left(H_0-\frac{2}{n+1}\frac{H_0ww^TH_0}{w^TH_0w}\right)
\end{cases}
$$

{{< /math >}}
{{< /callout >}}

## Onionification

{{< inline-svg "outline/barrier-block" >}} Under Construction!
