---
title: "Synergy Notes"
author: "John Zobolas"
date: "Last updated: 26 November, 2019"
knit: bookdown::render_book # to render the whole book not just this chapter
site: bookdown::bookdown_site
description: "Description"
url: 'https\://bblodfon.github.io/synergy-doc/'
github-repo: "bblodfon/synergy-doc"
bibliography: ["references.bib", "packages.bib"]
link-citations: true
---



# Intro {-}

Hi, there!

In the beginning I made these notes cause I found the need to clarify some things in my head regarding the mathematical models that underlie the drug combination world of synergistic effects and how these models have been used to computationally assess synergy, antagonism or non-interaction between drugs that are tested in high-throughput screens. 
Later I thought of making this as a bookdown [@R-bookdown] document since it would be much more nicier to have it in that format, even citable if need be and surely much more accessible to the scientific community than just having it in a plain MS Word file.

# Drugs and Effects: Terminology {-}

When a drug is administered in a biological system, we expect a measured output or effect which depends on the drug’s dosage ^[In this text, dosage and dose are equivalent terms and are used to describe the quantity of the administered drug used].
Usually, when we test drugs on cell lines, the measured output is the *viability* (response) of the cells, i.e. the percentage of the cells that survived. Generally, the following definitions can be used interchangeably:

  1. %Affected $f_a$, drug effect $E$, %death or %inhibition. Note that this definition closely relates to the drug effectiveness itself – how effective was the drug?
  2. %Unaffected $f_u$, viability, cell growth, survival, globaloutput $gl$(used in the DrugLogics pipeline ^[reference here at some point!]). Note that this definition relates to the *output on the system that the drug is used*: e.g. how much were the cells affected by the drug?

Note that the two definitions are complementary: $f_a+f_u \Rightarrow E+gl=1$.

# Dose-response curves (single drug) {-}

Drugs are administered in specific doses, so the drug’s effect is measured per each dosage. 
After the experiments are done, you end up with measurements for each drug in the form: $(x,y)$, where $x$ is the dosage and $y=E \in [E_min,E_max]$  the measured effect/viability/response (depending on which definition you use). 
I can plot these points to get the *dose-response* or *dose-effect* curve. 
Usually we assume that these curves are *monotonous* (always increasing or decreasing) though that may not always be true. 
There exist mathematical formulas that describe them, the most prominent of which is the **4-parameter log-logistic (4PL) model** [@Yadav2015]:

\begin{equation} 
  f\left(k\right) = \binom{n}{k} p^k\left(1-p\right)^{n-k}
  (\#eq:binom)
\end{equation}

See equation \@ref(eq:binom)

