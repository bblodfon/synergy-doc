# Introduction

## Drugs and Effects: Terminology {-}

When a drug is administered in a biological system, we expect a measured output or effect which depends on the drug’s dosage ^[In this text, *dosage* and *dose* are equivalent terms and are used to describe the quantity of the administered drug used].
Usually, when we test drugs on cell lines, the measured output is the *viability* (response) of the cells, i.e. the percentage of the cells that survived. Generally, the following definitions can be used interchangeably:

  1. *%Affected* $f_a$, drug effect $E$, *%death* or *%inhibition*. Note that this definition closely relates to the drug effectiveness itself – how effective was the drug?
  2. *%Unaffected* $f_u$, *viability*, *cell growth*, *survival*, *globaloutput* $gl$ (used in the DrugLogics pipeline ^[reference here at some point!]). Note that this definition relates to the *output on the system that the drug is used*: e.g. how much were the cells affected by the drug?

Note that the two definitions are complementary: $f_a+f_u \Rightarrow E+gl=1$.

## Dose-response curves (single drug) {-}

Drugs are administered in specific doses, so the drug’s effect is measured per each dosage. 
After the experiments are done, you end up with measurements for each drug in the form: $(x,y)$, where $x$ is the dosage and $y=E \in [E_{min},E_{max}]$  the measured effect/viability/response (depending on which definition you use). 
You can plot these points to get the *dose-response* or *dose-effect* curve. 
Usually we assume that these curves are *monotonous* (always increasing or decreasing) though that may not always be true ^[Experiments, experiments... I have seen dose-response curves that have *outliers*: so while the curve was monotonously descreasing, you have one point that creates a little step hill before ultimately going down!]. 
There exist mathematical formulas that describe them, the most prominent of which is the **4-parameter log-logistic (4PL) model** [@Yadav2015]:

\begin{equation} 
  E = \frac{E_{min}+E_{max}\left(\frac{x}{m}\right)^\lambda}{1+\left(\frac{x}{m}\right)^\lambda}
  (\#eq:4pmll)
\end{equation}

Note that $\lambda$ is the *sigmoidicity* of the curve and $m$ is the dosage of the drug that produces half the maximum effect (also defined in various texts as $EC_{50},IC_{50}$). For $E_{min}=0$, this equation is called *Hill’s equation*. 
A kind of derivative equation from \@ref(eq:4pmll) was proposed by [@Chou1984] and it’s called the **median effect equation** ^[This equation fits to the expectation of the mass-action law principle that dictates many biological processes such as cell growth or ligand-binding interactions – it’s the unified theory for the *Michaelis-Menten* equation, *Hill's* equation, *Henderson-Hasselbalch* equation and *Scatchard* equation [@Chou2006]]:

\begin{equation} 
  \frac{f_a}{f_u} = \frac{y-E_{min}}{E_{max}-y}=\left(\frac{x}{m}\right)^\lambda
  (\#eq:medeffeq)
\end{equation}

Where $f_a+f_u=1$. 
The goal when plotting this function is to find a way to measure the $m,\lambda$ parameters. 
[@Chou1984] proposed to rewrite equation \@ref(eq:medeffeq) as (generating what they called the *medial effect plot*):

\begin{equation}
  log\left(\frac{f_a}{1-f_a}\right)=\lambda\log x-\lambda\log m
  (\#eq:medeffplot)
\end{equation}

Where we can easily compute the $m,\lambda$ parameters (one is the *slope*, the other can be found where the plot cuts the $x$-axis: $y=log\left(\frac{f_a}{1-f_a}\right)=0$). 
Using Equation \@ref(eq:4pmll) and setting $E_{max}=1,E_{min}=0$ and as $x$ the $x/m$, we can see how the sigmoidicity parameter $\lambda$ affects the shape of the curve:

<div class="figure" style="text-align: center">
<img src="01-intro_files/figure-html/HillsPlot-1.png" alt="Hill's equation for different values of the slope parameter λ" width="576" />
<p class="caption">(\#fig:HillsPlot)Hill's equation for different values of the slope parameter λ</p>
</div>

Note that for $\lambda=1$ the shape is a *hyperbole*.

Also, using equation \@ref(eq:medeffeq), we can compute any dose $x$ as:

\begin{equation}
  x = m\left(\frac{f_a}{f_u}\right)^{1/\lambda} = m\left(\frac{y-E_{min}}{E_{max}-y}\right)^{1/\lambda}
  (\#eq:medeffeq2)
\end{equation}

## Drug Combinations and Dose-Response Matrices {-}

When doing experiments (usually referred to as **high-throughput screens**) with drug combinations ^[referring to combinations, we will mean 2 drugs for the rest of the text], specific dosages for each drug are tested and the combined effect is measured. 
The results are usually represented in a matrix form, where the $a_{i,j}$ element is the combined response, while the *labeling/name* of the $i$-row is the concentration of the first drug and the *labeling* of the $j$-column is the concentration of the second drug. 
From such a representation you can generate the *surface response model* and perform analyses using that 3D representation, which search for combinations of doses that produce larger combination effects [@Chou1984]. 
Another method plots the combination response vs the combined dosages of the two drugs (could be the sum of the doses for example), such that the description of the drug combination as synergistic or antagonistic is based on **visual comparison** between the single drug-response curves and the combined one, as is done in the CImbinator tool [@Flobak2017].

Most methodologies use a (mathematical) model that describes/calculates a response/effect threshold, which distinguishes synergy from non-synergy.
Thus, comparing each observed response with that threshold, we get a different synergy score value for each element of the dose-response matrix and then we can average these values (or use another method ^[Huge story here, should you take the average of the matrix, the average of a specific sub-matrix, the minimum, the median, a value that optimizes an expression, etc. I have seen most of these methods around papers. If you are looking for some examples, take a look at the *ExcessHSA*, *beta* ($\beta$), *gamma* ($\gamma$) and summary delta ($\Delta$) scores at the SI of [@MathewsGriner2014] and [@Yadav2015]]) to get **a single value for the whole dose-response matrix** – a *summary interaction score* that tells us if the combination was synergistic or not in the end. 
The models that describe how to define those thresholds (for each combination data point in the dose-response matrix for example) are discussed in the [next section](#null-reference-models).

## Null reference models {-}

Drugs produce effects. 
When drugs are used together (referred to as a *drug combination*) they can have greater or lesser effects (**synergy** or **antagonism**) than when used alone. 
To distinguish and categorize the combination effect we *compare* it to the effect that the drugs would have if they were used and **no interaction** was seen between them (also called the *additive effect*). 
A mathematical model that describes the *non-interaction* between two drugs is called a **null reference model** [@Lederer2018]. 
Every null-reference model defines an effect threshold, for which if we observe a **greater combination effect** we would call the interaction a synergy (an antagonism otherwise). Of course, the distinction does not need to be binary, e.g. the larger the combination effect is from the the additive threshold, the more synergistic the drug combination is (and vise-versa for the antagonism case).

There are **two kinds of null reference models**: the ones that are *effect-based* and the ones that are *dose-effect* based. 
The distinction is derived from what is used to define the specific thresholds that characterize a synergy effect: just the **effects** of the combined drugs or also information on their dosages (dose-response curves)? The most common null-reference models in each category are:

- Effect based
  - HSA (Highest Single Agent) ^[Also known as Gaddum’s non-interaction model]
  - Bliss Independence (Bliss)
  - Response additivity
- Dose-effect based
  - Loewe Additivity (Loewe)
  - ZIP Model
  - Explicit Mean Equation Model
  - Others
  
### Effect-based Models {-}

#### Combination Index (CI) {-}

### Dose-Effect based Models {-}

#### Loewe Additivity {-}

