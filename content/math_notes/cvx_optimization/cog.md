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

{{< callout context="danger" title="Todo Items" icon="outline/barrier-block" >}}Add plots and diagrams illustrating proof ideas (as toy examples).
{{< /callout >}}

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
- The volume inequality during the passage from {{< math >}}$\mathcal{S}_{t}${{< /math >}} to {{< math >}}$\mathcal{S}_{t+1}${{< /math >}} will be shown below - it is related to the so-called **Grünbaum Inequality**, which can be proved by also another famous inequality called **Brunn-Minkowski Inequality**.
- The _analytical complexity_ to guarantee an accuracy of {{< math >}}$O(\varepsilon)${{< /math >}} is {{< math >}}$O(m\log(2B\varepsilon^{-1}))${{< /math >}}. Compared to ellipsoid method's {{< math >}}$O(m^2\log(Rr^{-1}\varepsilon^{-1}))${{< /math >}}, both having _linear rate_ of convergence, it is less sensitive to the underlying dimension {{< math >}}$m${{< /math >}}.

## 2. Math Behind the COG Method

The heart of the COG method lies within _Brunn-Minkowski's inequality_ and _Grünbaum's inequality_. The latter inequality ensures that the peel we gain control of in each step of the COG method is large enough, while the first is an inequality relating two convex sets with their convex combination.

For the casual readers, you have already understand what the COG method does🎉!

For the more serious folks here, let us now dive into the beautiful maths.

### 2.1. Additional Notations

We introduce the following notations:

- Given {{< math >}}$X,Y\subset\mathbb{R}^m${{< /math >}} and {{< math >}}$Z\subset\mathbb{R}${{< /math >}}, we write:
  {{< math class="text-center">}}$$I(X,Y;Z)=\{(1-z)x+zy:(x,y,z)\in X\times Y\times Z\}$${{< /math >}}
  which is just a dirty notation for constructing cones, convex combinations. Some times we do not distinguish between elements and one-point sets.
- We write {{< math >}}$\nu_m:=\operatorname{vol}(B(O_m;1))${{< /math >}}, the volume of the unit ball (in {{< math >}}$\mathbb{R}^m${{< /math >}})
- Given a measurable subset {{< math >}}$X\subset\mathbb{R}^m${{< /math >}}, we write {{< math >}}$\rho_m(X):=\sqrt[m]{\operatorname{vol}(X)/\nu_m}${{< /math >}}, which satisfies:
  {{< math class="text-center">}}$$\operatorname{vol}(B(O_m;\rho_m(X)))=\operatorname{vol}(X)$${{< /math >}}
- Given {{< math >}}$X\subset\mathbb{R}^m${{< /math >}} with {{< math >}}$m\geq 2${{< /math >}}, we define {{< math >}}$X_{-}${{< /math >}} as the set of elements {{< math >}}$x\in X${{< /math >}} with {{< math >}}$x\cdot e_1\leq0${{< /math >}}. We define {{< math >}}$X_+${{< /math >}} analogously.
- Given {{< math >}}$X\subset\mathbb{R}^m${{< /math >}}, {{< math >}}$x\in\mathbb{R}${{< /math >}}, we can consider the slice:
  {{< math class="text-center">}}$$X_{u,:}=\{v\in\mathbb{R}^{m-1}:(u,v)\in X\}\subset\mathbb{R}^{m-1}$${{< /math >}}


### 2.2. Brunn-Minkowski Inequality

A good reference would be this one by R. J. Gardner's review[^3]. The Brunn-Minkowski inequality in the case of convex bodies can be stated concisely as follows[^4]:

[^3]: Gardner, Richard. "The Brunn-Minkowski Inequality." _Bulletin of the American mathematical society_ 39.3 (2002): 355-405.

{{< callout context="caution" title="Brunn-Minkowski Inequality" icon="outline/note" >}}

Fixed convex bodies {{< math >}}$A,B\subset\mathbb{R}^m${{< /math >}}.

1. **Additive.** The function {{< math >}}$\lambda\mapsto \rho_m(I(A,B;\lambda))${{< /math >}} is concave on {{< math >}}$(0, 1)${{< /math >}}.
2. **Multiplicative.** The function {{< math >}}$\lambda\mapsto \operatorname{vol}(I(A,B;\lambda))${{< /math >}} is log-concave on {{< math >}}$(0, 1)${{< /math >}}.

{{< /callout >}}

[^4]: For generalists, we remind that this theorem holds in much general settings. Our assumptions guarantees that {{< math >}}$I(A,B;\lambda)${{< /math >}} (which [is also a convex body](https://math.stackexchange.com/questions/2410875/the-minkowski-sum-of-two-convex-sets-is-convex)) [is measurable](https://math.stackexchange.com/questions/207609/the-measurability-of-convex-sets) with positive finite volume, which would avoid unfun cases.

We will show Item 1. Item 2 follows from Item 1[^5], by the fact that {{< math >}}$\log\circ\rho_m${{< /math >}} and {{< math >}}$\operatorname{log}\circ\operatorname{vol}${{< /math >}} differ by a constant, and that {{< math >}}$\log${{< /math >}}, {{< math >}}$\rho_m${{< /math >}} are concave on places we are interested. To show Item 1, it suffices to show the following:

{{< math class="text-center">}}$$\rho_m(A)+\rho_m(B)\leq\rho_m(A+B)$${{< /math >}}

By definition of Lebesgue measures, it suffices to show the case where {{< math >}}$A,B${{< /math >}} are finite union of sets of the form {{< math >}}$\bigtimes_{i=1}^m[a_i,b_i]${{< /math >}} (boxes). Write {{< math >}}$n_A,n_B${{< /math >}} as the least number of boxes needed to write {{< math >}}$A,B${{< /math >}} as union of boxes, and assume {{< math >}}$n_A\geq n_B${{< /math >}}. We prove by induction on {{< math >}}$n_A+n_B${{< /math >}}:

- **Base Case.** If {{< math >}}$n_A+n_B=2${{< /math >}}, may assume {{< math >}}$A=\bigtimes_{i=1}^m[0,a_i]${{< /math >}}, {{< math >}}$B=\bigtimes_{i=1}^m[0,b_i]${{< /math >}}, giving:
  {{< math class="text-center">}}$$\frac{\rho_m(A)+\rho_m(B)}{\rho_m(A+B)}=\sqrt[m]{\prod_{i=1}^m\frac{a_i}{a_i+b_i}}+\sqrt[m]{\prod_{i=1}^m\frac{b_i}{a_i+b_i}}\leq 1$${{< /math >}}
  by applying [AM-GM](https://en.wikipedia.org/wiki/AM%E2%80%93GM_inequality) to the {{< math >}}$\sqrt[m]{\cdot}${{< /math >}} terms.
- **Inductive Step.** By permuting and realignment, may assume {{< math >}}$A_{\pm}${{< /math >}}, {{< math >}}$B_{\pm}${{< /math >}} have positive measures, with {{< math >}}$n_{A_{\pm}}${{< /math >}} both being smaller than {{< math >}}$n_A${{< /math >}}, and that:
  {{< math class="text-center">}}$$\frac{\rho_m(A_{\pm})}{\rho_m(A)}=\frac{\rho_m(B_{\pm})}{\rho_m(B)}=\alpha_\pm\in(0,1)$${{< /math >}}
  which concludes the proof:
  {{< math class="text-center">}}
  \begin{align*}
  \frac{\rho(A+B)^m}{(\rho(A)+\rho(B))^m}&=\frac{\rho(A_{-} +B_{-})^m+\rho(A_{+} +B_{+})^m}{(\rho(A)+\rho(B))^m}\\
  &\geq\frac{(\rho(A_{-}) +\rho(B_{-}))^m+(\rho(A_{+}) +\rho(B_{+}))^m}{(\rho(A)+\rho(B))^m}\\
  &=\alpha_{-}^m+\alpha_{+}^m=1
  \end{align*}
  {{< /math >}}

[^5]: One can also show that multiplicative version implies the additive version. We don't need it here though.

{{< callout context="tip" title="Aside" icon="outline/bulb" >}}Another common way to prove it is to first use [_Prékopa–Leindler's inequality_](https://en.wikipedia.org/wiki/Pr%C3%A9kopa%E2%80%93Leindler_inequality) (specialized to characteristic functions) to establish the multiplicative version, then derive the additive version. The interested readers can consult this [lecture note](https://cs.uwaterloo.ca/~lapchi/cs798/L19.pdf).{{< /callout >}}

### 2.3. Grünbaum Inequality

I highly recommend checking out this [lecture note](https://cs.uwaterloo.ca/~lapchi/cs798/L19.pdf) from [this course](https://cs.uwaterloo.ca/~lapchi/cs798/) by [Lap Chi Lau](https://cs.uwaterloo.ca/~lapchi/).

{{< callout context="caution" title="Grünbaum Inequality" icon="outline/note" >}}
Given convex body {{< math >}}$X\subset\mathbb{R}^m${{< /math >}} with COG at {{< math >}}$O_m${{< /math >}}, we have {{< math >}}$\operatorname{vol}(X_{-})\geq e^{-1}\operatorname{vol}(X)${{< /math >}}.
{{< /callout >}}

The proof is a series of clever reductions to simpler cases. It would be beneficial to give definitions to these cases. Given a nonnegative function {{< math >}}$f${{< /math >}} with support a closed interval {{< math >}}$[a,b]\subset\mathbb{R}${{< /math >}} containing {{< math >}}$0${{< /math >}}, we can define a solid of revolution, given by:

{{< math class="text-center">}}$$Z_f:=\{(u,v)\in\mathbb{R}\times\mathbb{R}^{m-1}:u\in[a,b],\|v\|\leq f(u)\}$${{< /math >}}

Note that {{< math >}}$Z_f${{< /math >}} is convex iff {{< math >}}$f${{< /math >}} is concave. We will see that this is the entry point of Brunn-Minkowski's inequality in the proof of this theorem.

#### 2.3.1. Special Case: Cone

We show the inequality in the case of cones - that is, in the case where {{< math >}}$X=Z_f${{< /math >}} with {{< math >}}$f(a)=0${{< /math >}} and with {{< math >}}$f${{< /math >}} being linear. May assume {{< math >}}$a=-1,f(x)=x+1${{< /math >}}. We get {{< math >}}$b=m^{-1}${{< /math >}} by the following equation utilizing the condition that the COG of {{< math >}}$X${{< /math >}} is {{< math >}}$O_m${{< /math >}}:

{{< math class="text-center">}}$$
\int_{-1}^b(x+1)^{m-1}\nu_{m-1}x\mathrm{d}x=0
$${{< /math >}}

which gives:

{{< math class="text-center">}}
$$
\frac{\operatorname{vol}(Z_{f,-})}{\operatorname{vol}(Z_f)}=
\frac{\int_{-1}^0(x+1)^{m-1}\mathrm{d}x}{\int_{-1}^{1/m}(x+1)^{m-1}\mathrm{d}x}
=(1+m^{-1})^{-m}
\geq e^{-1}
$$
{{< /math >}}

#### 2.3.2. Special Case: Convex Solids of Revolution

Now we show the inequality in the case of solids of revolution. Suppose the convex body {{< math >}}$X${{< /math >}} has the form {{< math >}}$X=Z_f${{< /math >}}, then {{< math >}}$f${{< /math >}} is concave, say with support {{< math >}}$[a,b]${{< /math >}}. Associate to {{< math >}}$f${{< /math >}} a function {{< math >}}$g${{< /math >}}, with the following properties:

1. {{< math >}}$\operatorname{supp}(g)=[c,d]\subset\mathbb{R}${{< /math >}} with {{< math >}}$[c,d]${{< /math >}} containing {{< math >}}$0${{< /math >}}
2. {{< math >}}$g${{< /math >}} is non-negative, linear on {{< math >}}$[c,d]\subset\mathbb{R}${{< /math >}}
3. {{< math >}}$g(c)=0${{< /math >}}, {{< math >}}$g(0)=f(0)${{< /math >}}, {{< math >}}$\operatorname{vol}(Z_{f,\pm})=\operatorname{vol}(Z_{g,\pm})${{< /math >}}

then by concavity of {{< math >}}$f${{< /math >}} and these conditions, one can show that:
1. {{< math >}}$c\leq a\leq 0 \leq d\leq b${{< /math >}}
2. {{< math >}}$f${{< /math >}} dominates {{< math >}}$g${{< /math >}} on {{< math >}}$[a,0]${{< /math >}}.
3. {{< math >}}$g${{< /math >}} dominates {{< math >}}$f${{< /math >}} on {{< math >}}$[0,d]${{< /math >}}.

Therefore, the COG of {{< math >}}$Z_g${{< /math >}} is non-positive, so the special case for cones gives:

{{< math class="text-center">}}$$
\frac{\operatorname{vol}(Z_{f,-})}{\operatorname{vol}(Z)_f}=\frac{\operatorname{vol}(Z_{g,-})}{\operatorname{vol}(Z)_g}\geq e^{-1}
$${{< /math >}}

#### 2.3.3. General Case: Reduction to Solids of Revolution

For a general convex body {{< math >}}$X${{< /math >}}, consider the function {{< math >}}$f:\mathbb{R}\to[0,+\infty)${{< /math >}}, given by:
{{< math class="text-center">}}$$x\mapsto \rho_{m-1}(X_{x,:})$${{< /math >}}

By Brunn-Minkowski, it is a compactly-supported concave non-negative function, so by the identity {{< math >}}$\operatorname{vol}(X_{x,:})=\operatorname{vol}((Z_f)_{x,:})${{< /math >}}, we are done by considering the solid of revolution {{< math >}}$Z_f${{< /math >}}[^6]:

{{< math class="text-center">}}$$
\frac{\operatorname{vol}(X_{-})}{\operatorname{vol}(X)}=
\frac{\operatorname{vol}(Z_{f,-})}{\operatorname{vol}(Z_f)}\geq e^{-1}
$${{< /math >}}

[^6]: This is often called the "symmetrization" of {{< math >}}$X${{< /math >}} in the literatures.

