# Causal Inference

These are my notes taken while reading the book "Causal Inference: The Mixtape"

## Introduction

- Experimental data is collected in a lab
- Non-experimental / Observational data is collected through surveys, in a retrospective manner. 
- Causal Inference requires data with only 2 variables changing; one independent and other dependent. This is called _ceteris paribus_ ("all else constant")
- In economics, we only observe final price and quantity at equilibrium values and not the demand and supply curve. Demand ans Supply curves are only hypothetical.
- Price elasticity along a demand curve is $\frac{P}{Q}\frac{dQ}{dP}$ where $P,Q$ follow the demand curve.
- An econometric model is simply a model that predicts how variables vary with each other. For example, for demand curve is one such model and is given by $\ln Q_d = \alpha + \delta \ln P + \vec \gamma \vec x + u$ where $\vec x$ is a vector of other factors that determine the demand, such as pices of other goods. Here, $u\sim N(0,\sigma_u^2)$ is the error term, and $\delta$ is the elasticity. 
- Exogenicity is when $P$ is not dependent on $u$, basically $\text{Cov}(P,u) = 0$

## OLS

Given data of form $(x_i,y_i)$ where we have the relationship $y = \beta_0 + \beta_1 x + \mu$ , we can estimate $\beta_0,\beta_1$ as :

$$
\hat \beta_1 = \frac{\sum_{i}}{(x_i -\bar x)(y_i -\bar y)}{\sum_i (x_i - \bar x)^2} \\
\hat \beta_0 = \bar y - \hat \beta_1 \bar x 
$$

These are unbiased estimators of $\beta_1,\beta_0$.

From this, we can estimate the residuals as :

$$
\hat u_i = y_i - (\hat \beta_0 + \hat \beta_1 x_i) 
$$

A _mathematical_ proverty of OLS is that 

$$
\sum_i \hat u_i = 0
$$

This equation is exact. 

One can do OLS in R using `tidyverse` library as 

```R
tb <- tibble(
  x = 9*rnorm(10),
  u = 36*rnorm(10),
  y = 3 + 2*x + u,
  yhat = predict(lm(y ~ x)), # lazy evaluation allows this to work
  uhat = residuals(lm(y ~ x))
)
```

The function `lm` gives us a linear regression object, from which we can get the predictions and residuals. The `tibble` thing is just and advanced version of dataframes. All we are doing is passing things into a constructor. These keyword argument assignments will be then used for both the column names and values. 
In a tibble constructor call, you are supposed to pass "statements" and not "values". Essentially, the statement has its own scope which evaluates before handling results to the constructor. These results are not just simple values, but something like a Python dictionary. 

In Python, `pandas.DataFrame` objects have a method called `assign` that also does similar stuff to what's happening here. 

In R, `~` is the "Formula Operator" . This tells the `lm` function to model `y` as a function of `x`. This uses an intercept $\beta_0$ by default. To not do that, you should use `lm(y ~ x - 1)`. 
The fomula operator has its own syntax. For example, `y ~ .` will cause `lm` to use every other column in a data frame as independent variables and `y ~ x * z` will make it include `x`, `z` and the interaction `x : z` which basically means $x\cdot z$ in this case. Having `y ~ x : z` will use only the interaction and not `x` and `z` themselves. 

Another thing to keep in mind is that `lm` can either pick the data from the given context, (like when it's inside a `tibble` constructor) or have it passed inside. 

This is all very similar to SQL. 

For example, the code 

```R
tb <- tibble(
  x = 9*rnorm(10),
  u = 36*rnorm(10),
  y = 3 + 2*x + u,
  yhat = predict(lm(y ~ x)),
  uhat = residuals(lm(y ~ x))
)
```

would be written in SQL like 

```sql
SELECT 
    9 * RANDOM() AS x,
    36 * RANDOM() AS u,
    (3 + 2*x + u) AS y,
    predict(lm(y,x)),
    residuals(lm(y,x))
FROM DUAL --placeholder table
```

And the code 

```R
tibble(
    x = 9*rnorm(10000),
    u = 36*rnorm(10000),
    y = 3 + 2*x + u
  ) %>% 
    lm(y ~ x, .)
```

can be thought of as 

```sql
select 
    lm(y,x) from
(select
    9 * RANDOM() AS x,
    36 * RANDOM() AS u,
    (3 + 2*x + u) AS y
from dual)
```

You can even put all this crap inside a lambda function like so :

```R
function(x) tibble(
    x = 9*rnorm(10000),
    u = 36*rnorm(10000),
    y = 3 + 2*x + u
  ) %>% lm(y ~ x, .)
# This outputs lm objects
```

and then use this function inside a list comprehension :

```R
models <- lapply(
  1:1000,
  function(x) tibble(
    x = 9*rnorm(10000),
    u = 36*rnorm(10000),
    y = 3 + 2*x + u
  ) %>% lm(y ~ x, .)
)
```

To output coefficients, you access the `coeff` attribute like `coeff(model)` . You can do that for all models in `models` as

```R
sapply(models, coeff)
```

The function `sapply` is a wrapper around `lapply` which tries to output vectors and matrixes (homogenous data) rather than lists (in-homogenous data).

The output will be a wide matrix rather than a long matrix. So, we can take the transpose by accessing the `t` attribute as 

```R
t(sapply(models, coeff))
```

We might want to convert this to a tibble to print it. This can be done using the `as_tibble` function. 

Just as a reminder, the goodness-of-fit is computed as 

$$
R^2 = 1 - \frac{\text{SSR}}{\text{SST}} = 1- \frac{\sum_i \hat u_i ^2}{\sum _i (y_i - \bar y)^2} = \frac{\sum_i (\hat y_i - \bar y)}{\text{SST}}
$$

Now, onto the math details of OLS...

Remember that We actually write

$$
y(x) = \mu_{y|x} + u
$$

It's easy to see that $\hat y(x) = \mu_{y|x}$ is the model that will minimise the expected squared error, namely $E[(y-\hat y(x))^2]$ where the expectation is over both $x$ and $y$ . This can ofc be written as $E[E[(y-\hat y(x))^2 | x]]$, and so it clearly has the minimum when $\hat y (x) = \mu_{y|x}$.

Another thing to notice related to conditional variances and expectations is the ANOVA theorem (yes, this isn't jus a method, but also a theorem):

$$
\sigma^2_y = \text{Var}(\mu_{y|x}) + E[\sigma^2_{y|x}]
$$


The page just goes on and on, listing all the different properties of linear regression, and assumptions. 

The page defines a thing called "Robust standard errors" which are estimates of standard errors in the slope parameter when homoskedacity doesn't hold true. It's given as :

$$
\text{Var}(\hat \beta_1) = \frac{\sum_i (x_i - \bar x)^2 \sigma_i ^2}{(\sum_i x_i - \bar x)^2}
$$

Note that the estimators we had before are still unbiased. 

Then the page describes cluster robust standard errors. This was done in a really bad way and I didn't read this.

## DAG

Directed Acyclic Graphs are used to represent what causes what. The rule here is that causality runs in one direction only. 

A direct edge from a node $x$ to another node $y$ says that $x$ causes $y$, or that changes n $x$ necessarily lead to changes in $y$. But it doesn't say that changes in $y$ will lead to changes in $x$. 

A path joining $x$ to $y$ through some other nodes is called a _backdoor path_.
Suppose the backdoor path has the edge $(z,y)$, then we cannot just say that $z$ causes $y$ (although that is how we defined the edges..) since in the end, it is $x$ that causes $z$. So, we say that the relationship is _spurious_. Since $x$ confounds our ability to prove any relationship between $z$ and $y$, we say that it is a _confounder_ . 
All this terminology is context sensitive. For example, the path $x\to z\to y$ is a backdoor path if we are studying the relationship of $z$ on $y$, but apparently not a backdoor path but a "mediation" when we are studying effect of $x$ on $y$. 

To study the relationship now, you will need to _control_ (or condition) for $x$ (having only one value of $x$ in the dataset) and vary $z$ (which is supposed to vary $y$ too). This is called "closing a backdoor path". 

If there is a confounder that is unobserved/unknown, then we represent its effect on the affected nodes using dashed lines rather than solid lines. 
An unobserved confounder cannot be contolled for, since we can't measure its values. 

A collider is defined as a node in a potential backdoor path (if we don't account for directedness) that has flipped directions. This causes the path to be "closed". The reason for even studying this is because if we, for some reason tried to control a collider, then we would also be unknowingly creating a relationship between the variables that have a causal effect on it. For example, suppose you have a collider $C = X + Y + \epsilon$. The variables $X$ and $Z$ are known to be independent. But now, if you control the collider, then it creates relationships like $X = C -Y - \epsilon$ which now cause the relationship $Y \to X$ and similarly $X \to Y$. This can mess up your analysis. Why would you control a collider ? One would be because it's a mediator in some path and you got confused and tried to close that path. 
This effect I described is known as collider bias.  

The "backdoor criterion" simply means that all backdoor paths are closed either due to coliders or by controling the confounders. 

In practice, you don't control a confounder by actually keeping a fixed value for the dataset since that would mean tedious data collection. Instead, you estimate the effect of the confounder on the final independent variable. For example, if you are studying effect of $z$ on $y$, with confounder $x$, then you would use the (linear) model

$$
y = \alpha + \beta x + \delta z + \epsilon
$$

Then, you will use the coefficient $\delta$ in a statistical test to say whether or not the relationship between $y$ and $z$ is significant. 

## Potential outcomes

Suppose you do an experiment to see whether an intervention, say an internship improves the outcome, say the skill in software development. 

To get the data, you can simply get test 100 people who did an internship and 100 people who didn't and then do a t-test. 

The difference in the skill level of the two groups will be your proxy for "average treatment effect". 

Let's denote by $Y_i^0$ the skill of the person $i$ if he didn't do an internship and by $Y_i^1$, if he did. The quantity we want is $\delta_i = Y_i^1 - Y_i^0$ . Since only one of $Y_i^0 and Y_i^1$ will happen, we only have data for one. The other is unknown and is called the "counter-factual". 

Denote by $D_i$ the choice of the person, namely, whether he chose to do an internship $D_i = 1$ or not $D_i = 0$. This choice can be assumed to be rational, i.e. the person will only do an internship _if_ it improves the skill level. 

Now, rather than individuals, let's think of the two groups. 

What we are actually estimating (in a t-test, for example) is 

$$
E[Y^1|D = 1] - E[Y^0|D=0]
$$

But what we really want to compute is the average treatment effect :

$$
\text{ATE} = E[\delta] = E[Y^1] - E[Y^0]
$$

Denote by ATT and ATU, the average treatment effect conditioned on the groups that chose to be treated and the group that did not, i.e. 

$$
\text{ATT} = E[\delta | D = 1] = E[Y^1|D=1] - E[Y^0|D=0]\\
\text{ATU} = E[\delta | D = 0] = E[Y^1|D=0] - E[Y^0|D=0]\\
$$

Let's also define $p = E[D]$ as the fraction of individuals who chose to do an internship. 

In our setting we have : 

$$
\text{ATE} = p\text{ATT} + (1-p)\text{ATU} \\
= (1-p) (\text{ATU} - \text{ATT}) + \text{ATT} \\
= (1-p) (\text{ATU} - \text{ATT}) + E[Y^1|D=1] - E[Y^0|D=1] \\
= (1-p) (\text{ATU} - \text{ATT}) + (E[Y^0|D=0] - E[Y^0|D=1]) + (E[Y^1|D=1] - E[Y^0|D=0]) 
\\\implies 

(E[Y^1|D=1] - E[Y^0|D=0])  = \text{ATE} + (1-p) (\text{ATT} - \text{ATU}) + (E[Y^0|D=1] - E[Y^0|D=0]) \\
= \text{ATE} + (1-p) \text{DTE} + \text{SB}
$$

Here, $\text{DTE} = \text{ATT} - \text{ATU}$ is the difference is treatment effect (heterogenity) for different groups and $\text{SB}$ is the difference in the groups themselves (those who did not do an internship might have had a higher skill level already) . 

Note that 0 selection bias doesn't imply homogenous treatment effect. 

Consider two students who have to choose either to study for an examination ($D=1$) or not ($D=0$). Both students have exactly the same skill set and will thus score exactly the same in the exam if they don't study ($Y^0 \perp D$) . But if a student _chooses_ to study, as opposed to being forced to, then he will have the extra factor of motivation. Thus, $\delta \not \perp D$. So, say that the first one chooses to study and second doesn't. Then, when we will compute $(E[Y^1|D=1] - E[Y^0|D=0])$ for this ste-up, we'll still not get the actual effect of studying, since the first student also had motivation. To get the real effect, we'll have to _force_ the students to either study or not study, making $D$ exogenous (not a choice of the participant), which also makes $D \perp Y^1$. 

But commonly, when we say that there is no SB, we also implicitly say that there is not heterogenity. This is because $D$ can either be exogenous or endogenous. In the firs case it has zero DTE and SB, and in second case, both are (potentially) non-zero.

The selection bias arises because the individuals make rational choices according to the info at hand. To not have this happen, one can do 
- Physical randomisation, where the individauls are given the intervention at random, disregarding whether or not they need it. 
- Difference in Difference using pre-intervention and post-intervention data. This is usally more costly. 

Often, rather than using some approximation (say, using CLT) for the distribution of the test statistic, one can simply (under the null hypothesis) generate the distribution by shuffling/sampling the whole dataset into the control and experiment group in all possible manners and computing the test statistic for each permutation. The reason this works is because under the null hypothesis ($\delta =0$) the distributions for potential outcomes $Y^0$ and $Y^1$ are the same, and are thus the same as the actual values $Y$, and thus we can sample from the full data we have for $Y$ to generate the data for $Y^0$ and $Y^1$. Note thet this method requires $D \perp Y^0$ (no selection bias) and $D \perp \delta$ (no DTE) so that the actual case will actualy come from the distribution that is created from this bootstrap sampling procedure.  This can be done via the two methods. 

Of course, if normality holds (Anderson test passes for example), or if the data size is large, then this is not the best way to do it and it would, in general be better to use a simple t-test.  

## Subclassification

In subclassification, you have a list of confounding variables $\vec x$ that need to be controlled to study the relationship between the itervention $D$ and the outcome $Y$. 

The data you have at hand has different empirical distributions for $\vec x$ for the control group and the expriment group. 

So, you will estimate the ATE for each value of $\vec x$ and then take a weighted average (weighted by the amount of data for each $\vec x$ and the variances)

## Matching

In the case that $\vec x$ has high dimensions or has a very large range of values, there might be $\vec x$ values for which there are data-points in the experiment group, but not in the control group or vice versa. 

In this case, you can match each data point ($\vec x$) in the control groups with all points in the control group that are close enough (as per some distance metric for $\vec x$). If there are exact matches, go for those. 
In a sense, we are estimating the counterfactual for the data points. 
To get the ATE, rather than going over just the experiment group, you should go over the full dataset, estimating the counterfactual for each point as the average of close points from the other group. 

This still has the problem that the data from the other group used for matching may only match approximately, and thus cause bias for that particular $\vec x$. To remedy this, we can estimate the bias by fitting predictor models (e.g., using OLS) for $E[Y^0]( \vec x)$ and $E[Y^1](\vec x)$ based on $\vec x$, using data from the control group and experiment group respectively. 

## RDD

The regression discontinuity is a method that is applicable when the treatment $D$ is assigned to an individual based on some continuous metric $X$ going above a threshold value $c_0$ . 

In the most simple model, you have $D = 1(X > c_0)$. 

This means, using the switching equation, that :

$$
Y = E[Y^0|X] + (E[Y^1|X]-E[Y^0|X])1(X>c_0) + \epsilon
$$

One can then fit a model $\hat Y^0$ (usually OLS with quadratic basis) for $E[Y^0|X]$ and assume a constant ATE, namely $E[Y^1|X]-E[Y^0|X] = \delta$. This gives us : 

$$
D_i = 1(X_i>c_0) \\
Y_i = \hat Y^0(X_i) + \delta D_i + \epsilon_i
$$

This is really useful when data for $D_i$ isn't there somehow. 


For a more complicated model, you have :

$$
Z = 1(X > c_0) \\
\Pr(D|X) = \pi Z + f(X) + Zg(X) + \epsilon \\ 
\text{where} g(c_0) = 0
$$

Again, using the switching equation, this gives :

$$
E[Y|X] = E[Y^0|X] + \delta \Pr(D|X) \\
=  E[Y^0|X] + \delta \pi Z + \delta f(X) + \delta Z g(X) +\delta \epsilon
$$

Again, you go the same prediction model stuff. 

Except now, you have two equations :

$$
Z = 1(X > c_0) \\
\Pr(D|X) = \pi Z + f(X) + Zg(X) + \epsilon \\
E[Y|X] = \hat Y^0(X) + \delta \pi Z + \delta f(X) + \delta Z g(X)
$$

So now, you can simply divide the coefficents $\delta \pi$ and $\pi$ to get the ATE. 

In practice, this is done by eiher fitting OLS with upto quadratic basis one either side of $c_0$, or by using a kernel base approach to estimate this quantity :

$$
\frac{E[Y|X\to c_0^+] - E[Y|X\to c_0^-]}{E[D|X\to c_0^+] - E[D|X\to c_0^-]}
$$

## DiD

The basic DiD method just does the usual $D_1,D_2$ computation. Often we'll have multiple variables for the treatment, which will be represented by a vector $\vec D \in \{0,1\}^K$. We'll similarly have a vector for the ATT, i.e. $\vec \delta$ . For sake of simplicitly, let's NOT use this and just have one dimensional, binary treatment. 

The 2x2 DiD model has the form :

$$
Y_{it} = \alpha + \beta D_t + \gamma_i T_i +  \delta D_tT_i + \epsilon_{it}  
$$

Here, $T_i$ is an indicator of whether the unit is in the treatment group or not. And $D_t$ is the indicator of whether the current time is pre-treatment or post treatment. 

The $delta$ computed from this give us the ATT, only when there are parallel trends, namely $E[Y_{it}^0|D_t=1]-E[Y_{it}^0|D_t=0]$ is the same for both treatment and control groups. 

This model has only two states for time, pre-treatment and post-treatment. 

In actuality, there might be staggered adoption, and we will have many states for the time variable. 

The model to use now will be the two-way fixed-effects model. This assumes there are two kinds of effects to consider, one that varies across units (but not time), called $\alpha_i$ (e.g. earning ability) and other than varies accross time (e.g. market's status) that explain the deviation of the outcome (e.g. earning) $Y_{it}$. Moreover now, the treatment (e.g. education) $D_{it}$ can be switched on or off at any instance. 

The model is thus :

$$
Y_{it} = \alpha_0 + \delta D_{it} + \alpha_i + \alpha_t + \epsilon_{it}
$$

What this linear regression actually estimated for $\delta$ is given by the Bacon decomposition theorem. 

For simplicity, let's assume only three groups/units : 
- group $k$ that gets treated early at $T_k=2$, which means that $D_{kt} = 1(t \ge T_k)$
- group $l$ that gets treated later at $T_l=4$, which means that $D_{lt} = 1(t \ge T_l)$
- group $U$ that never gets treated(control group), i.e. for all $t$ from 1 to $T=5$, we have $D_{Ut}$ = 0 

With the simple model that we have, we define these quantites :

$$
\hat \Delta_{i} = \text{avg}(Y_i| t\ge T_i) - \text{avg}(Y_i| t<T_i) \\
\hat \delta_{ij} = \Delta_{i} - \Delta_{j} \\ 
\mu_{ij} = \frac{1-\text{avg}(D_i)}{1-(\text{avg}(D_i) - \text{avg}(D_l))} \\
\sigma^2_D = \hat {\text{Var}}(D_{it}) \\
s_{ij} = \frac{1}{V}n_in_l(\text{avg}(D_i) - \text{avg}(D_l))(1-(\text{avg}(D_i) - \text{avg}(D_l)))
$$

(AMBIGUOUS) Here, $n_i,n_j$ are the sample sizes of groups $i$ and $j$. 

Then, the OLS gives us :

$$
\hat \delta = 
\sum_{\{i,j\}} [s_{ij}(\mu_{ij}\hat \delta_{ij}^{(i)} + (1-\mu_{ij})\hat \delta_{ij}^{(j)})]
\\= \sum_{i}\sum_{j > i} [s_{ij}(\mu_{ij}\hat \delta_{ij}^{(i)} + (1-\mu_{ij})\hat \delta_{ij}^{(j)})]
$$

Notice the $s_{ii} = 0$, so the manipualation works.

WLOG, assume that $T_i < T_j$. We have these definitions :

$$
\hat \delta_{ij}^{(i)} = (\text{avg}(Y_{it} | D_{it} = 1 \land D_{jt}=0) - \text{avg}(Y_{it} | D_{it} = 0 \land D_{jt}=0)) - (\text{avg}(Y_{jt} | D_{it} = 1 \land D_{jt}=0) - \text{avg}(Y_{jt} | D_{it} = 0 \land D_{jt}=0)) \\
\hat \delta_{ij}^{(j)} = (\text{avg}(Y_{jt} | D_{it} = 1 \land D_{jt}=1) - \text{avg}(Y_{jt} | D_{it} = 1 \land D_{jt}=0)) - (\text{avg}(Y_{it} | D_{it} = 1 \land D_{jt}=1) - \text{avg}(Y_{it} | D_{it} = 1 \land D_{jt}=0)) 
$$

Notice that for $U$ (which doesn't have a $T_U$), the value $1-\mu_{iU}$ is 0 and thus, we don't care about $\delta_{iU}^{(U)}$. We may define it to be anything we want, and the decomposition will still work.  

Next, we can separate the terms with the control group $U$ involved and those where it isn't and thus get :

$$
\hat \delta = [\sum_{i\ne U} s_{iU}\hat \delta_{iU}] + \sum_{i\ne U}\sum_{j>i}[s_{ij}(\mu_{ij}\hat \delta_{ij}^{(i)} + (1-\mu_{ij})\hat \delta_{ij}^{(j)})]
$$

The difference of treatment groups as compared to the control groups are correct, and shoud be included. 

The value $\delta_{ij}^{(i)}$ is also correct, under the parallel trends assumption. 

Finally, the value $\delta_{ij}^{(j)}$ is only correct under the assumption of parallel trends and a treatment effect with isn't time varying. Because if that isn't true, then firstly, our model (the regression equation) is incorrect and secondly, the value of $Y_i$ will be different because of the time varying fixed effect ofc, and _because of time varying treatment_ in the pre-treatment ($[T_i,T_j]$) and post-treatment ($[T_i,T]$) periods (for $j$). This will cause a bias (which can't be killed like the variance by just increasing the sample size). 

To reduce this bias, we want $\mu_{ij}^{(j)}$ to be small. This can happen by treating $j$ much later so that we have $T - T_j \ll T_i$ . 

Another (probably better) thing we can do is have a time varying treatment effect in the model (ofc at that point, it's not the TWFE model). 