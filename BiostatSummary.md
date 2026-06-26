# Biostatistics Summary 
[Pranav Joshi](mailto:pranav.joshi@alumni.iitgn.ac.in)

### One sample stats

- std. dev: $s^2 = \frac{1}{n-1}\sum_i(X_i-\bar X)^2$
- Two sided confidence interval :
    $$ 
    X_L= \bar X - z_{(1-\alpha/2)}\frac{\sigma}{\sqrt n}\\
    X_H= \bar X + z_{(1-\alpha/2)}\frac{\sigma}{\sqrt n}
    $$
- Right tailed confidence interval $[X_L,\infty)$ used _after_ $H_A:\mu > 0$ is true. 
    $$ X_L = \bar X - z_{(1-\alpha)}\frac{\sigma}{\sqrt n}
    $$
- $\beta$ for right tailed test (right tailed dist. for $H_A$) : 
    $$ 
    c_\text{right} = \mu_0 + z_{(1-\alpha)}\sigma/\sqrt{n}\\ 
    \beta = \Phi(\frac{c_\text{right}-\mu_1}{\sigma /\sqrt{n}}) = \Phi((\mu_0-\mu_1)\frac{\sqrt n}{\sigma}+z_{(1-\alpha)}) \\ 
    1- \beta =1-\Phi(\dots) = \Phi(-\dots) = \Phi((\mu_1-\mu_0)\frac{\sqrt n}{\sigma}-z_{(1-\alpha)})
    $$
- $\beta$ for two sided test (use $\alpha/2$ everywhere) : 
    $$ 
    \beta = \Phi(\frac{c_\text{right}-\mu_1}{\sigma /\sqrt{n}}) - \Phi(\frac{c_\text{left}-\mu_1}{\sigma /\sqrt{n}}) \\
    = \Phi(\frac{(\mu_0-\mu_1)\sqrt{n}}{\sigma}+z_{(1-\alpha/2)}) - \Phi(\frac{(\mu_0-\mu_1)\sqrt{n}}{\sigma}-z_{(1-\alpha/2)}) \\
    = \Phi(\frac{(\mu_1-\mu_0)\sqrt{n}}{\sigma}+z_{(1-\alpha/2)}) - \Phi(\frac{(\mu_1-\mu_0)\sqrt{n}}{\sigma}-z_{(1-\alpha/2)})
    $$ 
- power curve is the $(1-\beta)$ vs $\mu_1$ curve
- _Minimum_ sample size $n$ given $\alpha,\beta_{max}$ for right tailed test:
   $$
    \sqrt{n} \ge \sigma \frac{z_{(1-\alpha)}+z_{(1-\beta_\text{max})}}{\mu_1-\mu_0}
   $$
- _Sufficient_ sample size $n$ given $\alpha,\beta_{max}$ for two tailed test:
   $$
    \sqrt{n} \ge \sigma \frac{z_{(1-\alpha/2)}+z_{(1-\beta_\text{max})}}{\mu_1-\mu_0}
   $$

<div style="page-break-after: always;"></div>

### Two sample parametric

- Paired data : 
  - convert to single variable $d_i = X_{1,i}-X_{2,i}$ and do normal z-test or t-test.
  - For sufficient sample size, use $\delta'-0 =\delta'$ in denominator in place of $``\mu_1-\mu_0"$
  - Use $t_{P}$ instead of $z_{P}$ in numerator if t-test
  - In case normality test fails for $d_i$, do Sign test or Wilcoxon Signed-Rank test
- Independent sample z-test (both equal and equal variances):
   $$
    Z = \frac{\bar X_1 -\bar X_2}{\sqrt{\frac{\sigma_1^2}{n_1} + \frac{\sigma_2^2}{n_2}}} \sim N(0,1)
   $$
   For right tailed test 
   $$
    \delta' = \mu_1 - \mu_2\\
    1-\beta = \Phi(\frac{\delta'-z_{(1-\alpha)}\sqrt{\frac{\sigma_1^2}{n_1} + \frac{\sigma_2^2}{n_2}}}{\sqrt{\frac{\sigma_1^2}{n_1} + \frac{\sigma_2^2}{n_2}}}) \\
    \text{both } \sqrt{n_1},\sqrt{n_2} \ge \sqrt{n_{suff}} = [\frac{(z_{(1-\alpha)}+z_{(1-\beta_{max})})\sqrt{\sigma_1^2+\sigma_2^2}}{\delta'} ]
   $$
- Independent sample t-test (unequal variances):
  $$
  t = \frac{\bar X_1 - \bar X_2}{\sqrt{(s_1^2/n_1)+(s_2^2/n_2)}} \sim T_\text{Welch}(\nu) \\\,\\
  \nu = \frac{(\frac{s_1^2}{n_1}+\frac{s_2^2}{n_2})^2}{\frac{s_1^4}{n_1^2(n_1-1)}+\frac{s_2^4}{n_2^2(n_2-1)}}
  $$
- Independent sample t-test (equal variances):
  $$
  s_p = \sqrt{\frac{(n_1-1)s_1^2+(n_2-1)s_2^2}{(n_1-1)+(n_2-1)}} \\
  t = \frac{\bar X_1-\bar X_2}{s_p\sqrt{\frac{1}{n_1}+\frac{1}{n_2}}} \sim T_\text{Student}(n_1+n_2-2)
  $$

<div style="page-break-after: always;"></div>

### Multiple sample stats

- ANOVA ($k$ groups, $N$ total points)
  $$
  \bar X = \frac{1}{N}\sum X_{i,j} = \frac{1}{N}\sum_j n_j X_j \\
  (k-1)s_B^2 = \text{SBB}=\sum_j n_j(\bar X_j-\bar X)^2 \\ 
  (N-k)s_W^2 = \text{SSW}= \sum_j(n_j-1)s_j^2 \\ 
  (N-1)s_T^2 = \text{SST} = \sum_{i,j}(X_{i,j}-\bar X)^2 \\ 
  \text{SST} = \text{SSB} + \text{SSW} \\ 
  f := \frac{s_B^2}{s_W^2} \sim F_{(k-1),(N-k)}
  $$

- Multiple comparisons ($k$ groups, $N$ total points)
  
  $$
  t_{j_{1},j_{2}} = \frac{\bar X_{j_1} -\bar X_{j_2}}{s_W\sqrt{\frac{1}{n_{j_1}}+\frac{1}{n_{j_2}}} } \quad \text{where} \quad s_W^2 = \frac{1}{N-k}\sum_j(n_j-1)s_j^2 \\\,\\
  \alpha = 1-(1-\alpha')^{\binom{k}{2}} \implies \alpha \le \binom{k}{2} \alpha' \quad [\because \text{Bernoulli's inequality}] \\\,\\
  \alpha' = \frac{\alpha_{max}}{\binom{k}{2}} \quad [\text{Bonferroni}]
  $$ 

<div style="page-break-after: always;"></div>

### Two sample non-parametric paired

- Sign test
  - Compute $d_i = X_{1,i} - X_{2,i}$ (paired data)
  - Remove all data with $d_i = 0$. Remaining is size $n$.
  $$
  H_0 : \delta_\text{median} = 0, \quad H_A : \delta_\text{median} \ne 0 \\\,\\
  D = \sum_i \text{pos}(d_i) \sim \text{Binom}(n,1/2) \\
  Z = \frac{D-n/2}{\sqrt {n/4}}
  $$
  - If $n$ is large, $p = 2(1-\Phi(|Z|))$
  - If $n$ is small ($np < 5$ or $n(1-p) < 5$):
    $$
    p = \sum_{r=0}^{\min(n-D,D)} \binom n r 2^{-n} + \sum_{r=\max(n-D,D)}^{n} \binom n r 2^{-n}  
    $$
- Wilcoxon Signed Rank Test
  - Compute $d_i = X_{1,i} - X_{2,i}$ (paired data)
  - Remove all data with $d_i = 0$. Remaining is size $n$.
  - Testing for $\quad H_A : \delta_\text{median} \ne 0$
  - Rank $|d_i|$ (absolute differences) to get $r_i$. Use avg rank to break ties
  - $T = \sum_i r_i\, \text{pos}(d_i)$
  $$
  \mu_T = \frac{n(n+1)}{4} \\ 
  \sigma_T = \sqrt{\frac{n(n+1)(2n+1)}{24}}\\ 
  Z = \frac{T-\mu_T}{\sigma_T} \sim_{n\gg 1} N(0,1)
  $$
  - Convention : Use the group that gives smaller $T$ (keep that as group 1 or use "neg" instead of "pos").

<div style="page-break-after: always;"></div>

### Non-parametric independent sample

- Wilcoxon Rank-Sum Test
  - Unpaired data. Testing to see if medians are unequal ($H_A : m_1 \ne m_2$)
  - Combine into one array, and rank with avg. rank for tie breaking.
  - Sum the ranks to compute ranksums, smaller of which is $W$
  $$
  \mu_W = \frac{n_S(n_S+n_L+1)}{2}\,, \quad
  \sigma_W = \sqrt{\frac{n_S n_L(n_S+n_L+1)}{12}} \\\,\\
  Z = \frac{W-\mu_W}{\sigma_W} \sim N(0,1)
  $$

- Kruskal Walis Test
  - Unpaired data with $N$ total points and $k$ groups. 
  - Testing to see if medians are unequal
  $$
  H_0 : m_j = m \,\forall\, j\,, \quad
  H_A : \exists j_1,j_2 \text{ s.t. } m_{j_1} \ne m_{j_2}
  $$
  - Combine into one array, and rank with avg. rank for tie breaking.
  - Sum the ranks to compute ranksums $R_j$
  - Test statistic
  $$
  H = -3(N+1)+\frac{12}{N(N+1)}\sum_{j=1}^k \frac{R_j^2}{n_j} \sim \chi^2(k-1)
  $$

<div style="page-break-after: always;"></div>

### Correlation

- Pearson Correlation Test 
  - $H_A : \rho \ne 0$
  $$
  r = \frac{1}{n-1}\sum_i (\frac{X_i-\bar X}{s_X})(\frac{Y_i-\bar Y}{s_Y}) \\\,\\
  t = r \sqrt {\frac{n-2}{1-r^2}} \sim T_\text{Student}(n-2)
  $$

- Spearman Rank Correlaton
  - Rank $X_i$ separately to get ranks $A_i$
  - Rank $Y_i$ separately to get ranks $B_i$
  - The Pearson correlation of the ranks is the $r_s$. More efficient:
  $$
  r_s = 1 - \frac{6\sum_i (A_i-B_i)^2}{(n-1)(n)(n+1)}
  $$
  - Test statistic is same as Pearson
  $$
  t_s = r_s\sqrt {\frac{n-2}{1-r_s^2}} \sim T_\text{Student}(n-2)
  $$

<div style="page-break-after: always;"></div>

### Regression

- General Regression ($n$ sample size, $k$ model parameters)
  - Mean Squared Prediction Error (MSPE) is $E_Y[(Y-\hat Y(x))^2]$. This is a function of $x$
  - $\sigma_{Y|x}^2 = E_Y[(Y-\mu_{Y|x})^2] \le \text{MSPE}$
  - MSPE is estimated by the square of "sample standard deviation from regression"
  $$
  s_{Y|X} =\sqrt{\frac{1}{n-k}\sum_i (\hat y_i - y_i)^2}
  $$
  Note that $E[s^2_{Y|x}] = \text{MSPE}$ and not $E[s^2_{Y|x}] = \sigma^2_{Y|x}$.
  - Coefficient of determination $$ R^2 = 1- \frac{\text{SSE}}{\text{{SST}}} = 1- \frac{(n-k)s_{Y|x}^2}{(n-1)s_Y^2} $$
    For simple linear regression, $R^2 = r^2$

- Homoskedacity (HS)
  - $\text{Var}(Y|x) = \sigma^2_{Y|x}$ is constant (as a function of $x$)
  - $E[Y|x] = \mu_{Y|x}$ does change with $x$
  - Decomposition of variance
  $$
  \sigma^2_Y = \sigma^2_{Y|X} + E_X[(\mu_{Y|X}-\mu_Y)^2]
  $$

- Bivariate Normal Distribution (BND)
  $$
  E[Y|X] = \mu_Y + \rho \frac{\sigma_Y}{\sigma_X} (X-\mu_X) \\
  \text{BND}\implies\text{HS}\implies
  \rho^2 = 1-\frac{\sigma^2_{Y|X}}{\sigma_Y^2} \\
  $$

<div style="page-break-after: always;"></div>

### Linear Regression

- Simple Linear Regression
  - Assumes BND for $(X,Y)$ to get linear model
  $$
  \beta_1 = \rho \frac{\sigma_Y}{\sigma_X}\,,\quad 
  \beta_0 = \mu_Y - \rho \frac{\sigma_Y}{\sigma_X}\mu_X = \mu_Y - \beta_1\mu_X \\\,\\
  \mu_{Y|X} = \mu_Y + \rho  \frac{\sigma_Y}{\sigma_X} (X-\mu_X) = \beta_0 + \beta_1 X
  $$
  - Estimates
  $$
  \hat \beta_1 = r\frac{s_Y}{s_X} = \frac{\sum_i (x_i-\bar x)(y_i-\bar y)}{\sum_i (x_i-\bar x)^2}\,, \quad
  \beta_0 = \bar y - \hat \beta_1 \bar x \\\,\\
  \text{se}(\hat \beta_1) = \sqrt {E[(\hat \beta_1 -\beta_1)^2]} = \frac{\sigma_{Y|X}}{s_X\sqrt{n-1}}= \frac{\sigma_{Y|X}}{\sqrt{\sum_i (x_i-\bar x)^2}} \\\,\\
  \text{se}(\hat \beta_0) = \sqrt {E[(\hat \beta_0 -\beta_0)^2]} = \sigma_{Y|X}\sqrt{\frac{1}{n}+\frac{\bar x^2}{(n-1)s_X^2}} = \sigma_{Y|X}\sqrt{\frac{1}{n}+\frac{\bar x^2}{\sum_i (x_i-\bar x)^2}}
  $$
  - Estimates of error in estimates
  $$
  \hat{\text{se}}(\hat \beta_1) = \frac{s_{Y|X}}{s_X\sqrt{n-1}}\,, \quad
  \hat{\text{se}}(\hat \beta_0) = s_{Y|X}\sqrt{\frac{1}{n}+\frac{\bar x^2}{(n-1)s_X^2}}
  $$
  - Coefficient of determination
  $$
  r^2 = R^2 = 1 - \frac{(n-2)s_{Y|X}^2}{(n-1)s_Y^2}
  \implies \frac{s_Y}{s_{X|Y}} = \frac{1}{\sqrt{1-r^2}}\frac{\sqrt{n-2}}{\sqrt{n-1}}
  $$

- Testing SLR models
  Given the linear model $\hat Y_T(X) = \beta_{00} + \beta_{10}X$ and data $x_i,y_i$
  $$
  H_{A,0} : \beta_0 \ne \beta_{00}\,, \quad H_{A,1} : \beta_1 \ne \beta_{10} \\
  H_{0,0}:\beta_0 = \beta_{00}\,, \quad H_{0,1}:\beta_1 = \beta_{10} \\
  t_0 = \frac{\hat \beta_0 - \beta_{00}}{\hat{\text{se}}(\hat \beta_0)}, \quad
  t_1 = \frac{\hat \beta_1 - \beta_{10}}{\hat{\text{se}}(\hat \beta_1)}
  $$
  Under $H_{0,0},H_{0,1}$, we have $t_0,t_1 \sim T_\text{Student}(n-2)$
  
- SLR parameter significance
  Set $\beta_{00} = \beta_{10} = 0$ in the SLR model test.
  $$
  t_0 = \frac{\hat \beta_0}{\hat{\text{se}}(\hat \beta_0)}\,, \quad
  t_1 = \frac{\hat \beta_1}{\hat{\text{se}}(\hat \beta_1)} = \frac{r\sqrt{n-2}}{\sqrt{1-r^2}} \\\,\\
  H_{0,1}:\beta_1=0 \iff H_{0,corr}:\rho =0 
  $$

