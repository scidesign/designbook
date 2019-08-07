# Completely Randomized Designs: Comparing More Than Two Treatments

## ANOVA - Comparing more than two groups

The following example is taken from Chapter 4 @bhh2005. The table below gives coagulation times for blood samples drawn from 24 animals receiving four different diets A, B, C, and D.




                      A    B    C    D
------------------  ---  ---  ---  ---
                     60   65   71   62
                     63   66   66   60
                     59   67   68   61
                     63   63   68   64
                     62   64   67   63
                     59   71   68   56
Treatment Average    61   66   68   61
Grand Average        64   64   64   64
Difference           -3    2    4   -3


Boxplots of the data are shown below.


```r
boxplot(y~diets,data = tab0401,xlab = "Diets",
        ylab = "Coagulation time",
        main = "Coagulation time from 24 \n animals randomly allocated to four diets")
```

<img src="07-anova_files/figure-html/unnamed-chunk-2-1.png" width="672" />



**Question:** Is there evidence to indicate a difference in mean coagulation times for the four different diets?

An idea due to Fisher is to compare the variation in mean coagulation times *between* the diets to the variation of coagulation times *within* a diet. These two measures of variation are often summarized in an analysis of variance (ANOVA) table.   


## Analysis of Variance (ANOVA) table

The between treatments variation and within treatment variation are two components of the total variation in the response.

In the coagulation study data we can break up each observation's deviation from the grand mean into two components: treatment deviations; and residuals within treatment deviations.

$$y_{ij}-{\bar y}_{\cdot \cdot}=\left(y_{i \cdot}-{\bar y}_{\cdot \cdot}\right)+\left(y_{ij}-{\bar y}_{i \cdot}\right)$$

Let $y_{ij}$ be the $jth$ observation taken under treatment $i = 1,...,a$. $$E(y_{ij})=\mu_i=\mu+\tau_i,$$ and $Var(y_{ij})=\sigma^2$ and the observations are mutually independent.  The parameter $\tau_i$ is the $ith$ treatment effect. 

We are interested in testing if the $a$ treatment means are equal.

$$H_0: \mu_1=\cdots=\mu_a \hspace{0.5cm}\text{vs.}\hspace{0.5cm}  H_1: \mu_i \ne \mu_j, \thinspace i \ne j.$$ 

There will be $n$ observations under the $ith$ treatment.

$$ y_{i\cdot}=\sum_{j = 1}^n y_{ij}, \hspace{1cm} {\bar y}_{i\cdot}=y_{i\cdot}/n,$$

$$ y_{\cdot \cdot}=\sum_{i = 1}^a \sum_{j = 1}^n y_{ij}, \hspace{1cm} {\bar y}_{\cdot \cdot}=y_{\cdot \cdot}/N,$$

where $N = an$ is the total number of observations.  The "dot"  subscript notation means sum over the subscript that it replaces.
 
## The ANOVA identity

The total sum of squares $SS_{T}= \sum_{i = 1}^a \sum_{j = 1}^n \left(y_{ij}- {\bar y}_{\cdot \cdot}\right)^2$ can be written as

$$ \sum_{i = 1}^a \sum_{j = 1}^n \left[({\bar y}_{i\cdot} - {\bar y}_{\cdot \cdot}) + (y_{ij}- {\bar y}_{i \cdot})\right]^2$$
 
by adding and subtracting ${\bar y}_{i\cdot}$ to $SS_T$.  


It can be shown that 

$$ \begin{aligned}
SS_T = \sum_{i = 1}^a \sum_{j = 1}^n \left(y_{ij}-{\bar y}_{\cdot \cdot}\right)^2 &= \underbrace{n\sum_{i = 1}^a \left(\bar{y_{i \cdot}}-{\bar y}_{\cdot \cdot}\right)^2}_{\text{Sum of Squares Due to Treatment}} + \underbrace{\sum_{i = 1}^a \sum_{j = 1}^n \left(y_{ij}-{\bar y}_{i \cdot} \right)^2}_{\text{Sum of Squares Due to Error}} \label{eq1} \\
   &= SS_{Treat} + SS_E.
\end{aligned}$$

This is sometimes called the analysis of variance identity.  It shows how the total sum of squares can be split into two sum of squares: one part that is due to differences between treatments; and one part due to differences within treatments.

For example, the decomposition of the first observation $y_{11}=60$ in diet A is 

$$\begin{aligned}
y_{11}-{\bar y}_{\cdot \cdot}&=\left(y_{1 \cdot}-{\bar y}_{\cdot \cdot}\right)+\left(y_{11}-{\bar y}_{1 \cdot}\right) \\
60-64&=(61-64)+(60-61)\\
-4 &=-3+-1
\end{aligned}$$



### Example - Blood coagulation study

The deviations from the grand average $\left(y_{ij}-{\bar y}_{\cdot \cdot}\right)$  are in the table below:


```
  A  B C  D
 -4  1 7 -2
 -1  2 2 -4
 -5  3 4 -3
 -1 -1 4  0
 -2  0 3 -1
 -5  7 4 -8
```

The total sum of squares is obtained by squaring all the entries in this table and summing:  $SS_T=(-4)^2+(-1)^2 + \cdots + (-8)^2=$ 340.

The between treatment deviations $\left(y_{i \cdot}-{\bar y}_{\cdot \cdot}\right)$ are in the table below:


```
  A B C  D
 -3 2 4 -3
 -3 2 4 -3
 -3 2 4 -3
 -3 2 4 -3
 -3 2 4 -3
 -3 2 4 -3
```

The sum of squares due to treatment is obtained by squaring all the entries in this table and summing: $SS_{Treat} = (-3)^2 + (2)^2 + \cdots +(-3)^2=$ 228.

The within treatment deviations $\left(y_{ij}-{\bar y}_{i \cdot} \right)$ are in the table below:


```
  A  B  C  D
 -1 -1  3  1
  2  0 -2 -1
 -2  1  0  0
  2 -3  0  3
  1 -2 -1  2
 -2  5  0 -5
```

The sum of squares due to error $\left(y_{ij}-{\bar y}_{i \cdot} \right)$ is obtained by squaring the entries in this table and summing:  $SS_E=(-1)^2+(2)^2+\cdots+(-5)^2=$ 112. 

$$\underbrace{340}_{SS_T} =\underbrace{228}_{SS_{Treat}}+\underbrace{112}_{SS_E}.$$

Which illustrates the ANOVA identity for the blood coagulation study.

The deviations 

- $SS_{Treat}$ is called the sum of squares due to treatments (i.e., between treatments), and $SS_E$ is called the sum of squares due to error (i.e., within treatments).
- There are $an = N$ total observations.  So $SS_T$ has $N-1$ degrees of freedom.
- There are $a$ treatment levels so $SS_{Treat}$ has $a-1$ degrees of freedom.
- Within each treatment there are $n$ replicates with $n-1$ degrees of freedom.  There are $a$ treatments.  So, there are $a(n-1)=an-a = N-a$ degrees of freedom for error. 
 
$$SS_E= \sum_{i = 1}^a \left[\sum_{j = 1}^n \left(y_{ij}-{\bar y}_{i \cdot} \right)^2\right]$$

If the term inside the brackets is divided by $n-1$ then it is the sample variance for the $ith$ treatment

$$S_i^2=\frac{\sum_{j = 1}^n \left(y_{ij}-{\bar y}_{i \cdot} \right)^2}{n-1}, \hspace{1cm} 1 = 1,...,a.$$

Combining these $a$ variances to give a single estimate of the common population variance

$$\frac{(n-1)S_1^2+ \cdots + (n-1)S_a^2}{(n-1)+ \cdots + (n-1)}=\frac{SS_E}{N-a}.$$

Thus, $SS_E$ is a pooled estimate of the common variance $\sigma^2$ within each of the $a$ treatments.

If there were no differences between the $a$ treatment means ${\bar y}_{i \cdot}$ we could use the variation of the treatment averages from the grand average to estimate $\sigma^2$.

$$\frac{SS_{Treat}}{a-1}$$

is an estimate of $\sigma^2$ when the treatment means are all equal.
 
The analysis of variance identity gives two estimates of $\sigma^2$.  One is based on the variability within treatments and one based on the variability between treatments.  If there are no differences in the treatment means then these two estimates should be similar.  If these estimates are different then this could be evidence that the difference is due to differences in the treatment means. 

The mean square for treatment is defined as

$$MS_{Treat}=\frac{SS_{Treat}}{a-1}$$

and the mean square for error is defined as

$$MS_E=\frac{SS_E}{N-a}.$$

$SS_{Treat}$ and $SS_E$ are independent and it can be shown that $SS_{Treat}/\sigma^2 \sim \chi^2_{a-1}$ and $SS_E/\sigma^2 \sim \chi^2_{N-a}$.  Thus, if $H_0:  \mu_1=\cdots=\mu_a$ is true then the ratio

$$ F= \frac{MS_{Treat}}{MS_E} \sim F_{a-1,N-a}.$$


The ANOVA table for the coagulation data can be calculated in R.


```r
aov.diets <- aov(y~diets,data = tab0401)
summary(aov.diets)
```

```
            Df Sum Sq Mean Sq F value   Pr(>F)    
diets        3    228    76.0   13.57 4.66e-05 ***
Residuals   20    112     5.6                     
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```

In this example $a-1 = 3, N-a = 20, SS_{Treat}=228, SS_E = 112, MS_{Treat}=228/3 = 76.0,MS_E112/20 = 5.6, F = 76/5.6 = 13.57.$

The observed $F$ value of 13.57 is shown on the $F_{3,20}$ distribution.  The p-value of the test is the area under the density to the right of 13.57 (red line).  The 95% critical value of the $F_{3,20}$ is 3.10 (blue line).  In other words, $P(F_{3,20}>3.10)=0.05$.


```r
x <-seq(0,20,by = 0.01)
plot(x,df(x = x,df1 = 3,df2 = 20),type = "l",ylab = "F(3,20) Density",main = "F(3,20) Distribution")
abline(v = 13.57,col = "red")
abline(v = qf(p = 0.95,3,20),col = "blue")
```

<img src="07-anova_files/figure-html/unnamed-chunk-7-1.png" width="672" />


The p-value could also be calculated directly using the cdf of the $F_{3,20}$ distribution.


```r
1-pf(q = 13.57,df1 = 3,df2 = 20)
```

```
[1] 4.66169e-05
```

The small p-value indicates that the difference between at least one pair of the treatment means is significantly different from 0.


## General ANOVA

The general form of the ANOVA table is

Source of variation | Degrees of freedom | Sum of squares | Mean square | F
--------------------|--------------------|----------------|-------------|--
Between treatments  | $a-1$              | $SS_{Treat}$   | $MS_{Treat}$|
Within treatments   | $N-a$              | $SS_E$         | $MS_E$      | $F=\frac{MS_{Treat}}{MS_E}$

## ANOVA Assumptions

The calculations that make up an ANOVA table require no assumptions. You could write 24 numbers in the ANOVA table and complete the table using the ANOVA identity and definitions of mean square and F statistic. However, using these numbers to make inferences about differences in treatment means will require certain assumptions.


1. Additive model.

$$y_{ij}=\mu+\tau_i+\epsilon_{ij}.$$

The parameters $\tau_i$ are interpreted as the treatment effect of the $i^{th}$ mean.  That is, if $\mu_i$ is the mean of $i^{th}$ group and $\mu$ is the overall mean then $\tau_i=\mu_i-\mu$.


2.  Under the assumption that the errors $\epsilon_{ij}$ are independent and identically distributed (iid) with common variance $Var(\epsilon_{ij})=\sigma^2$, for all $i,j$ then

$$E(MS_{Treat})=\sum_{i = 1}^a \tau_i^2 + \sigma^2, \hspace{1cm} E(MS_E)=\sigma^2.$$

If there are no differences between the treatment means then $\tau_1=\cdots=\tau_4 = 0$ and $\sum_{i = 1}^a \tau_i^2 = 0$ then both $MS_{treat}$ and $MS_E$ would be estimates $\sigma^2$.


3. If $\epsilon_{ij} \sim N(0,\sigma^2)$ then $MS_{Treat}$ and $MS_E$ are independent.  Under the null hypothesis that $\sum_{i = 1}^a \tau_i^2 = 0$ the ratio $F=\frac{MS_{Treat}}{MS_E}$ is the ratio of two independent estimates of $\sigma^2$.  Therefore, $\frac{MS_{Treat}}{MS_E} \sim F_{a-1,N-a}.$

### Example - checking the assumptions in the blood coagualtion study

1. The additive model assumption seems plausible since the observations from each diet can be viewed as the sum of a common mean plus a random error term.

2. The common variance assumption can be investigated by plotting the residuals versus the fitted values of the ANOVA model.  A plot of the residuals versus fitted values can be used to investigate the assumption that the residuals are randomly distributed and have constant variance. Ideally, the points should fall randomly on both sides of 0, with no recognizable patterns in the points.In the R this can be done using the following commands.


```r
plot(aov.diets$fitted.values,aov.diets$residuals,ylab = "Residuals",
     xlab = "Fitted",main = "Blood coagualtion study")
abline(h = 0)
```

<img src="07-anova_files/figure-html/unnamed-chunk-9-1.png" width="672" />

The assumption of constant variance is satisfied for the blood coagulation study.

3. The normality of the residuals can be investigated using a normal quantile-quantile plot.


```r
qqnorm(aov.diets$residuals, main = "Normal Q-Q Plot for blood coagulation study")
qqline(aov.diets$residuals)
```

<img src="07-anova_files/figure-html/unnamed-chunk-10-1.png" width="672" />

The normality assumptions is satisfied.


## Coding Qualitative Predictors in Regression Models

A dummy or indicator variable in a regression takes on a finite number of values so that different categories of a nominal variable can be identified. The term dummy reflects the fact that the values taken on by such variables (e.g., 0, 1, -1) do not indicate meaningful measurements but rather categories of interest. (Kleinbaum et al., 1998)

Examples of dummy variables are:

$$X =
\left\{
	\begin{array}{ll}
		1  & \mbox{if treatment A } \\
		0 & \mbox{otherwise}
	\end{array}
\right.$$

$$Y =
\left\{
	\begin{array}{ll}
		1  & \mbox{if subject is male } \\
	 -1 & \mbox{if subject is female}
	\end{array}
\right.$$

The variables $X$ and $Y$ are nominal variables describing treatment group and sex respectively.  

The following rule should be applied to avoid collinearity in defining a dummy variable for regression analysis: if the nominal independent variable of interest has $k$ categories then exactly $k-1$ dummy variables should be defined to index the categories if the regression model contains an intercept term.

### Dummy Coding

Dummy coding compares each level to the reference level.  The intercept is the mean of the reference group.

Smarties is a candy that comes in several different colours such as yellow, purple, green, and pink. Suppose that we would like to compare the mean number of candy colours in each box.  The data from 3 smarties boxes are below.


```r
count <- c(4,3,4,3,1,4,2,5,1,1,2,4)
colour <- as.factor(c(rep("Yellow",3),rep("Purple",3),
                      rep("Green",3),rep("Pink",3)))
```


colour    count
-------  ------
Yellow        4
Yellow        3
Yellow        4
Purple        3
Purple        1
Purple        4
Green         2
Green         5
Green         1
Pink          1
Pink          2
Pink          4

The average number of candies in each colour is:


```r
#Get means for each flavour
sapply(split(count,colour),mean)
```

```
   Green     Pink   Purple   Yellow 
2.666667 2.333333 2.666667 3.666667 
```

Dummy coding is the default in R and the most common coding scheme.  It compares each level of the categorical variable to a fixed reference level. 


```r
contrasts(colour) <- contr.treatment(4)
contrasts(colour)  # print dummy coding - base is Green
```

```
       2 3 4
Green  0 0 0
Pink   1 0 0
Purple 0 1 0
Yellow 0 0 1
```

Green is the reference category.  The first column compares Pink to Green, the second column compares Purple to Green, and the third column compares Yellow to Green.  The the three columns define three dummy variables:

$$X_1 =
\left\{
	\begin{array}{ll}
		1  & \mbox{if smartie is pink } \\
		0 & \mbox{otherwise}
	\end{array}
\right.$$

$$X_2 =
\left\{
	\begin{array}{ll}
		1  & \mbox{if smartie is purple } \\
		0 & \mbox{otherwise}
	\end{array}
\right.$$

$$X_3 =
\left\{
	\begin{array}{ll}
		1  & \mbox{if smartie is yellow } \\
		0 & \mbox{otherwise}
	\end{array}
\right.$$

If $X_1 = X_2 = X_3 = 0$ then the colour of the smartie is green - the reference category.  This shows that we only require 3 dummy variables to define a nominal variable with 4 categories.

To change the reference level change the value of base in `contr.treatment()`.



```r
contrasts(colour) <- contr.treatment(4,base = 2) # Now reference is pink
contrasts(colour)  
```

```
       1 3 4
Green  1 0 0
Pink   0 0 0
Purple 0 1 0
Yellow 0 0 1
```

```r
contrasts(colour) <- contr.treatment(4,base = 3) # Now reference is purple
contrasts(colour)  
```

```
       1 2 4
Green  1 0 0
Pink   0 1 0
Purple 0 0 0
Yellow 0 0 1
```

```r
contrasts(colour) <- contr.treatment(4,base = 4) # Now reference is yellow
contrasts(colour)  
```

```
       1 2 3
Green  1 0 0
Pink   0 1 0
Purple 0 0 1
Yellow 0 0 0
```


### Deviation Coding

This coding system compares the mean of the dependent variable for a given level to the overall mean of the dependent variable.  Consider the dummy variables

The the three columns define three dummy variables:

$$X_1 =
\left\{
	\begin{array}{ll}
		1  & \mbox{if smartie is green } \\
		-1 & \mbox{if smartie is yellow} \\
		0 & \mbox{otherwise}
	\end{array}
\right.$$

$$X_2 =
\left\{
	\begin{array}{ll}
		1  & \mbox{if smartie is pink } \\
		-1 & \mbox{if smartie is yellow} \\
		0 & \mbox{otherwise}
	\end{array}
\right.$$

$$X_3 =
\left\{
	\begin{array}{ll}
		1  & \mbox{if smartie is purple } \\
		-1 & \mbox{if smartie is yellow} \\
		0 & \mbox{otherwise}
	\end{array}
\right.$$

1 is used to compare a level to all other levels and -1 is assigned to yellow because it's the level that will never be compared to the other levels.

In R the variables can be created using the `contr.sum()` function.  The argument of 4 in `contr.sum(4)` indicates the number of levels of the factor.


```r
contrasts(colour) <- contr.sum(4)
contrasts(colour)  
```

```
       [,1] [,2] [,3]
Green     1    0    0
Pink      0    1    0
Purple    0    0    1
Yellow   -1   -1   -1
```

## Estimating Treatment Effects using Least Squares 

Let $y_{ij}$ be the $j^{th}$ observation under the $i^{th}$ treatment, and $\mu$ be the overall mean.  The model for diet $$y_{ij}=\mu+\tau_i+\epsilon_{ij}$$, $\epsilon_{ij} \sim N(0,\sigma^2)$$ can be written in terms of the dummy variables $X_1, X_2, X_3$ as:

$$ y_{ij}=\mu+\tau_1X_{i1}+\tau_2X_{i2}+\tau_3X_{i3}+\epsilon_{ij},$$

where,  

$$X_{1j} =
\left\{
	\begin{array}{ll}
		1  & \mbox{if jth unit recieves diet 2 } \\
		0 & \mbox{otherwise}
	\end{array}
\right.$$

$$X_{2j} =
\left\{
	\begin{array}{ll}
		1  & \mbox{if jth unit recieves diet 3 } \\
		0 & \mbox{otherwise}
	\end{array}
\right.$$

$$X_{3j} =
\left\{
	\begin{array}{ll}
		1  & \mbox{if jth unit recieves diet 4 } \\
		0 & \mbox{otherwise}
	\end{array}
\right.$$

It follows that $E(y_{Aj})=\mu_A=\mu$ is the mean of diet A so 

$$\begin{aligned}
E(y_{Bj})=\mu_B=\mu_A+\tau_1 &\Rightarrow \tau_1=\mu_B-\mu_A \\ 
E(y_{Cj})=\mu_C=\mu_A+\tau_2 &\Rightarrow \tau_2=\mu_C-\mu_A \\ 
E(y_{Dj})=\mu_D=\mu_A+\tau_3 &\Rightarrow \tau_3=\mu_D-\mu_A   
\end{aligned}$$


The least squares estimates are: 

$$\begin{aligned}
{\hat \mu}&={\bar y}_{1 \cdot}, \\
{\hat \tau_1}&={\bar y}_{2 \cdot}-{\bar y}_{1 \cdot}, \\
{\hat \tau_2}&={\bar y}_{3 \cdot }-{\bar y}_{1 \cdot}, \\
{\hat \tau_3}&={\bar y}_{3 \cdot }-{\bar y}_{1 \cdot}.
\end{aligned}$$

This model can also be written in matrix notation $y = X\beta+\epsilon$, where $\beta=\left(\mu,\tau_1,\tau_2,\tau3 \right), X=({\bf 1},X_{i1},X_{i2},X_{i3})$, and $\epsilon=(\epsilon_{ij})$. $X$ is an $30 \times 4$ design matrix with ${\bf 1}$ is a $30\times 1$ column vector of 1s, and $\epsilon$ is an $30 \times 1$ column vector.  Note that $\tau_4$ corresponding to the 4th treatment is implicitly set to 0.  It is used as a constraint so that that $(X'X)^{-1}$ exists.


## Using the `lm()` Function in R to Estimate Treatment Effects 

Let's return to the blood coagulation study. The table below gives coagulation times for blood samples drawn from 24 animals receiving four different diets A, B, C, and D.



                      A    B    C    D
------------------  ---  ---  ---  ---
                     60   65   71   62
                     63   66   66   60
                     59   67   68   61
                     63   63   68   64
                     62   64   67   63
                     59   71   68   56
Treatment Average    61   66   68   61
Grand Average        64   64   64   64
Difference           -3    2    4   -3



```r
attach(tab0401)
contrasts(diets)
```

```
  B C D
A 0 0 0
B 1 0 0
C 0 1 0
D 0 0 1
```

```r
lm.diets <- lm(y~diets,data = tab0401)
summary(lm.diets)
```

```

Call:
lm(formula = y ~ diets, data = tab0401)

Residuals:
   Min     1Q Median     3Q    Max 
 -5.00  -1.25   0.00   1.25   5.00 

Coefficients:
              Estimate Std. Error t value Pr(>|t|)    
(Intercept)  6.100e+01  9.661e-01  63.141  < 2e-16 ***
dietsB       5.000e+00  1.366e+00   3.660  0.00156 ** 
dietsC       7.000e+00  1.366e+00   5.123 5.18e-05 ***
dietsD      -9.999e-15  1.366e+00   0.000  1.00000    
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 2.366 on 20 degrees of freedom
Multiple R-squared:  0.6706,	Adjusted R-squared:  0.6212 
F-statistic: 13.57 on 3 and 20 DF,  p-value: 4.658e-05
```

The design matrix is


```r
model.matrix(lm.diets)
```

```
   (Intercept) dietsB dietsC dietsD
1            1      0      0      0
2            1      0      0      0
3            1      0      0      0
4            1      0      0      0
5            1      0      0      0
6            1      0      0      0
7            1      1      0      0
8            1      1      0      0
9            1      1      0      0
10           1      1      0      0
11           1      1      0      0
12           1      1      0      0
13           1      0      1      0
14           1      0      1      0
15           1      0      1      0
16           1      0      1      0
17           1      0      1      0
18           1      0      1      0
19           1      0      0      1
20           1      0      0      1
21           1      0      0      1
22           1      0      0      1
23           1      0      0      1
24           1      0      0      1
attr(,"assign")
[1] 0 1 1 1
attr(,"contrasts")
attr(,"contrasts")$diets
[1] "contr.treatment"
```

The default dummy coding was used.

The averages for each of the four diets are in the table below.

Diet | A ($j = 1$) | B ($j = 2$) | C ($j = 3$) | D ($j = 4$)
-----|---|---|---|---
Average (${\bar y}_{j \cdot})$| 61 | 66 | 68| 61|


So we can verify that the least-squares estimates are differences of the treatment averages.

$$\begin{aligned}
{\bar y}_{1 \cdot}&=61, \\ 
{\hat \tau_1}&={\bar y}_{2 \cdot}-{\bar y}_{1 \cdot}=5 \\ 
{\hat \tau_2}&={\bar y}_{3 \cdot }-{\bar y}_{1 \cdot}=7 \\ 
{\hat \tau_3}&={\bar y}_{3 \cdot }-{\bar y}_{1 \cdot}=-9.9 \times 10^{-15}.
\end{aligned}$$

If deviation coding was used then the parameter estimates would represent different treatment effects.  In the regression model the dummy variables would be defined as 

$$X_1 =
\left\{
	\begin{array}{ll}
		1  & \mbox{if diet is A } \\
		-1 & \mbox{if diet is D} \\
		0 & \mbox{otherwise}
	\end{array}
\right.$$

$$X_2 =
\left\{
	\begin{array}{ll}
		1  & \mbox{if diet is B } \\
		-1 & \mbox{if diet is D} \\
		0 & \mbox{otherwise}
	\end{array}
\right.$$

$$X_3 =
\left\{
	\begin{array}{ll}
		1  & \mbox{if diet is C } \\
		-1 & \mbox{if diet is D} \\
		0 & \mbox{otherwise}
	\end{array}
\right.$$


It follows that 

$$\begin{aligned}
E(y_{Aj})&=\mu_A=\tau_0+\tau_1 \\
E(y_{Bj})&=\mu_B=\tau_0+\tau_2 \\
E(y_{Cj})&=\mu_C=\tau_0+\tau_3 \\
E(y_{Dj})&=\mu_D=\tau_0-\tau_1-\tau_2-\tau_3
\end{aligned}$$

So,

$$\begin{aligned}
\tau_0 &= \frac{\mu_A+\mu_B+\mu_C+\mu_D}{4} \\
\tau_1 &= \mu_A - \frac{\mu_A+\mu_B+\mu_C+\mu_D}{4} \\
\tau_2 &= \mu_B - \frac{\mu_A+\mu_B+\mu_C+\mu_D}{4} \\
\tau_3 &= \mu_C - \frac{\mu_A+\mu_B+\mu_C+\mu_D}{4} \\
\end{aligned}$$



```r
contrasts(tab0401$diets) <- contr.sum(4)
lm.diets <- lm(y~diets,data = tab0401)
summary(lm.diets)
```

```

Call:
lm(formula = y ~ diets, data = tab0401)

Residuals:
   Min     1Q Median     3Q    Max 
 -5.00  -1.25   0.00   1.25   5.00 

Coefficients:
            Estimate Std. Error t value Pr(>|t|)    
(Intercept)  64.0000     0.4830 132.493  < 2e-16 ***
diets1       -3.0000     0.8367  -3.586 0.001849 ** 
diets2        2.0000     0.8367   2.390 0.026781 *  
diets3        4.0000     0.8367   4.781 0.000114 ***
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 2.366 on 20 degrees of freedom
Multiple R-squared:  0.6706,	Adjusted R-squared:  0.6212 
F-statistic: 13.57 on 3 and 20 DF,  p-value: 4.658e-05
```

The estimate of the intercept $\hat \tau_0$ is the grand average, and the slope estimates $\hat{\tau_1}, \hat{\tau_2}, \hat{\tau_3}$ are the differences between the treatment averages and grand average for diets A, B, C, D.


## Multiple Comparisons

Suppose that experimental units were randomly assigned to three treatment groups.  The hypothesis of interest is:

$$H_0: \mu_1=\mu_2 =\mu_3 \thinspace {\text  vs. } \thinspace H_1: \mu_i \ne\mu_j.$$ 

Now, suppose that we reject $H_0$ at level $\alpha$.  Which pairs of means are significantly different from each other at level $\alpha$?  There are ${3 \choose 2}=3$ possibilities. 

1. $\mu_1 \ne \mu_2$
2. $\mu_1 \ne \mu_3$
3. $\mu_2 \ne \mu_3$

Suppose that $k = 3$ separate (independent) hypothesis level $\alpha$ tests are conducted

$$H_{0_k}: \mu_i=\mu_j  \thinspace {\text  vs. } \thinspace H_{1_k}: \mu_i \ne\mu_j,$$ 

When $H_0$ is true, $P\left(\text{reject } H_0 \right)=\alpha \Rightarrow 1- P\left(\text{do not reject } H_0 \right)=1-\alpha$.  So, if $H_0$ is true then

$$\begin{aligned}
P\left(\text{reject at least one } H_{0_k} \right) &= 1- P\left(\text{do not reject any } H_{0_k} \right) \\
                                               &= 1- P\left(\text{do not reject } H_{0_1} \text{and } \text{do not reject } H_{0_2} \text{and } \text{do not reject } H_{0_3}  \right) \\
                                               &= 1- P\left(\text{do not reject } H_{0_1}\right)P\left(\text{do not reject } H_{0_2}\right)P\left(\text{do not reject } H_{0_3}\right) \hspace{0.3cm} \\
                                               &= 1-(1-\alpha)^{3}
\end{aligned}$$

If $\alpha = 0.05$ then the probability that at least one $H_0$ will be falsely rejected is $1-(1-.05)^3 = 0.14$, which is almost three times the type I error rate.

In general if $$H_0: \mu_1=\mu_2 = \cdots =\mu_k \thinspace {\text  vs. } \thinspace H_1: \mu_i \ne\mu_j.$$ 

If $c$ independent hypotheses are conducted then the probability 

$$P\left(\text{reject at least one } H_{0_k} \right) = 1-(1-\alpha)^c$$

is called the **family-wise error rate**.

The **pairwise error rate** is $P\left(\text{reject } H_{0_k} \right)=\alpha$ for any $c$. 

The multiple comparison problem is that multiple hypotheses are tested level $\alpha$ which increases the probability that at least one of the hypotheses will be falsely rejected (family-wise error rate).  

When groups are significantly different from ANOVA researchers often wish to explore where the differences lie.  Is it appropriate to test for differences looking at all pairwise comparisons?

- Testing all possible pairs increases the type I error rate.
- This means the chance that there is a higher probability,  beyond the pre-stated type I error rate (e.g. 0.05), that that a significant difference is detected when the truth is that no difference exists.



### The Bonferroni Method

To test for the difference between the $ith$ and $jth$ treatments, it is common to use the two-sample $t$ test. The two-sample $t$ statistic is

$$ t_{ij}= \frac{\bar{y_{j \cdot}}-\bar{y_{i \cdot}} } {\hat{\sigma}\sqrt{1/n_j+1/n_i}},$$

where $\bar{y_{j \cdot}}$ is the average of the $n_i$ observations for treatment $j$ and $\hat{\sigma}$ is $\sqrt{MS_E}$ from the ANOVA table.

Treatments $i$ and $j$ are declared significantly different at level $\alpha$ if

$$|t_{ij}|>t_{N-k,\alpha/2},$$

where $t_{N-k,\alpha/2}$ is the upper $\alpha/2$ percentile of a $t_{N-k}$.

The total number of pairs of treatment means that can be tested is $$c={k \choose 2}=\frac{k(k-1)}{2}.$$

The Bonferroni method for testing $H_0:\mu_i=\mu_j$ vs. $H_0:\mu_i \ne \mu_j$ rejects $H_0$ at level $\alpha$ if 

$$|t_{ij}|>t_{N-k,\alpha/2c},$$

where $c$ denotes the number of pairs being tested.

In R the function `pairwise.t.test()` can be used to compute Bonferroni adjusted p-values.  

This is illustrated below for the blood coagulation study.


```r
pairwise.t.test(tab0401$y,tab0401$diets,p.adjust.method = "bonferroni")
```

```

	Pairwise comparisons using t tests with pooled SD 

data:  tab0401$y and tab0401$diets 

  A       B       C      
B 0.00934 -       -      
C 0.00031 0.95266 -      
D 1.00000 0.00934 0.00031

P value adjustment method: bonferroni 
```

There are significant differences at the 5% level between diets A and B, A and C, B and D, and C and D using the Bonferroni method.

For comparison the unadjusted p-values are also calculated.


```r
pairwise.t.test(tab0401$y,tab0401$diets,p.adjust.method = "none")
```

```

	Pairwise comparisons using t tests with pooled SD 

data:  tab0401$y and tab0401$diets 

  A       B      C      
B 0.0016  -      -      
C 5.2e-05 0.1588 -      
D 1.0000  0.0016 5.2e-05

P value adjustment method: none 
```

The significant differences are the same using the unadjusted p-values but the p-values are larger then the p-values adjusted using the Bonferroni method.

A 100$(1-\alpha)$% simultaneous confidence interval for $c$ pairs $\mu_i-\mu_j$ is

$$\bar{y_{j \cdot}}-\bar{y_{i \cdot}} \pm t_{N-k,\alpha/2c}\hat{\sigma}\sqrt{1/n_j+1/n_i}.$$

After identifying which pairs are different, the confidence interval quantifies the range of plausible values for the differences.

The treatment means can be obtained from the table below.


                      A    B    C    D
------------------  ---  ---  ---  ---
                     60   65   71   62
                     63   66   66   60
                     59   67   68   61
                     63   63   68   64
                     62   64   67   63
                     59   71   68   56
Treatment Average    61   66   68   61
Grand Average        64   64   64   64
Difference           -3    2    4   -3

${\hat \sigma}=\sqrt{MS_E}$ can be obtained from the ANOVA table.  


```r
anova(lm(y~diets,data = tab0401))
```

```
Analysis of Variance Table

Response: y
          Df Sum Sq Mean Sq F value    Pr(>F)    
diets      3    228    76.0  13.571 4.658e-05 ***
Residuals 20    112     5.6                      
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```

The upper $.05/(2\cdot 6)=0.004$ percentile of the $t_{24-4}$ can be obtained with the t quantile function in R `qt()`.


```r
qt(p = 1-0.004,df = 20)
```

```
[1] 2.945349
```

Plugging in these values to the confidence interval formula we can obtain a Bonferroni adjusted 95% confidence interval for $\mu_B-\mu_A$:

$$ 66-61 \pm 2.95 \sqrt{5.6} \sqrt{1/6+1/6}$$

The lower and upper limits can be calculated in R.


```r
66-61 - qt(p = 1-0.004,df = 20)*sqrt(5.6)*sqrt(1/6+1/6) # lower limit
```

```
[1] 0.9758869
```

```r
66-61 + qt(p = 1-0.004,df = 20)*sqrt(5.6)*sqrt(1/6+1/6) # upper limit
```

```
[1] 9.024113
```

The 95% confidence interval for $\mu_B-\mu_A$ is ( 0.98, 9.02 ).



### The Tukey Method

The only difference between the Tukey and Bonferroni methods is in the choice of the critical value.  

Treatments $i$ and $j$ are declared significantly different at level $\alpha$ if

$$|t_{ij}|>\frac{1}{\sqrt 2} q_{k,N-k,\alpha},$$

where $t_{ij}$ is the observed value of the two-sample t-statistic and $q_{k,N-k,\alpha}$ is the upper $\alpha$ percentile of the Studentized range distribution with parameters $k$ and $N-k$ degrees of freedom.  The CDF and inverse CDF of the Studentized Range Distribution is available in R via the functions `ptukey()` and `qtukey()` respectively.

A 100$(1-\alpha)$% simultaneous confidence interval for $c$ pairs $\mu_i-\mu_j$ is

$$\bar{y_{j \cdot}}-\bar{y_{i \cdot}} \pm \frac{1}{\sqrt 2} q_{k,N-k,\alpha} \hat{\sigma}\sqrt{1/n_j+1/n_i}.$$

The Bonferroni method is more conservative than Tukey's method. In other words, the simultaneous confidence intervals based on the Tukey method are shorter.

In the coagulation study $N = 24, k = 4$ so the 5% critical value of the Studentize range distribution is obtained using the the inverse CDF function `qtukey()` for this distribution. The argument `lower.tail = FALSE` is used so we obtain the upper percentile of the distribution (i.e., the value of $x$ such that $P\left(X>x\right)=0.05$). 


```r
qtukey(.05,4,16,lower.tail = FALSE)
```

```
[1] 4.046093
```

Let's obtain the Tukey p-value and confidence interval for $\mu_B-\mu_A$.  The observed value of the test statistic is 

$$q^{obs}=\sqrt{2}|t_{AB}|,$$

where $$t_{AB}=\frac{\bar{y_{A \cdot}}-\bar{y_{B \cdot}} } {\hat{\sigma}\sqrt{1/n_A+1/n_B}}.$$


```r
(sqrt(2)*(66-61))/(sqrt(5.6)*sqrt(1/6+1/6))
```

```
[1] 5.175492
```

The p-value 

$$P\left(q_{4,20}>q^{obs}\right)$$

is then obtained using the CDF of the Studentized range distribution


```r
1-ptukey(q = sqrt(2)*5/sqrt(2*5.6/6),nmeans = 4,df = 20)
```

```
[1] 0.007797788
```

The 95% limits of the Tukey confidence interval for $\mu_B-\mu_A$ is


```r
5-(1/sqrt(2))*qtukey(p = .05,nmeans = 4,df = 20,lower.tail = FALSE)*sqrt(5.6)*sqrt(1/6+1/6) #lower limit
```

```
[1] 1.175925
```

```r
5+(1/sqrt(2))*qtukey(p = .05,nmeans = 4,df = 20,lower.tail = FALSE)*sqrt(5.6)*sqrt(1/6+1/6) #upper limit
```

```
[1] 8.824075
```

The width of the Tukey confidence interval for $\mu_B-\mu_A$ is


```r
(1/sqrt(2))*qtukey(p = .05,nmeans = 4,df = 20,lower.tail = FALSE)*sqrt(5.6)*sqrt(1/6+1/6)
```

```
[1] 3.824075
```

The width of Bonferroni $\mu_B-\mu_A$ is


```r
qt(p = 1-0.004,df = 20)*sqrt(5.6)*sqrt(1/6+1/6)
```

```
[1] 4.024113
```


This shows that the Tukey confidence interval is shorter than Bonferroni confidence intervals.

The command `TukeyHSD()` can be used to obtain all the Tukey confidence intervals and p-values for an ANOVA.  

Continuing with the blood coagulation study all of the 95% Tukey confidence intervals for the diets are


```r
TukeyHSD(aov(y~diets,data = tab0401))
```

```
  Tukey multiple comparisons of means
    95% family-wise confidence level

Fit: aov(formula = y ~ diets, data = tab0401)

$diets
             diff        lwr       upr     p adj
B-A  5.000000e+00   1.175925  8.824075 0.0077978
C-A  7.000000e+00   3.175925 10.824075 0.0002804
D-A -1.421085e-14  -3.824075  3.824075 1.0000000
C-B  2.000000e+00  -1.824075  5.824075 0.4766005
D-B -5.000000e+00  -8.824075 -1.175925 0.0077978
D-C -7.000000e+00 -10.824075 -3.175925 0.0002804
```

A plot of the 95% confidence intervals can be obtained by using the `plot()` function.


```r
plot(TukeyHSD(aov(y~diets,data = tab0401)))
```

<img src="07-anova_files/figure-html/unnamed-chunk-34-1.png" width="672" />


## Sample size for ANOVA - Designing a study to compare more than two treatments 

Consider the hypothesis that k means are equal vs. the alternative that at least two differ. What is the probability that the test rejects if at least two means differ? Power = $1-P({\text{Type II error}})$ is this probability.

The null and alternative hypotheses are:

$$H_0: \mu_1=\mu_2 = \cdots = \mu_k \thinspace {\text  vs. } \thinspace H_1: \mu_i \ne\mu_j.$$ 

The test rejects at level $\alpha$ if

$$MS_{Treat}/MS_E \ge F_{k-1,N-K,\alpha}.$$

The power of the test is

$$ 1- \beta= P\left(MS_{Treat}/MS_E \ge F_{k-1,N-K,\alpha} \right),$$

when $H_0$ is false.  

When $H_0$ is false it can be shown that:

- $MS_{Treat}/\sigma^2$ has a non-central Chi-square distribution with $k-1$ degrees of freedom and non-centrality parameter $\delta$.

- $MS_{Treat}/MS_E$ has a non-central $F$ distribution with the numerator and denominator degrees of freedom $k-1$ and $N-k$ respectively, and non-centrality parameter 

$$\delta = \frac{\sum_{i = 1}^kn_i\left(\mu_i-{\bar \mu} \right)^2}{\sigma^2},$$

where $n_i$ is the number of observations in group $i$, ${\bar \mu}=\sum_{i = 1}^k \mu_i/k$, and $\sigma^2$ is the within group error variance .

This is denoted by $F_{k-1,N-k}(\delta)$.

### Direct calculation of Power using R

- The power of the test is 

$$P\left(F_{k-1,N-k}(\delta) > F_{k-1,N-K,\alpha} \right).$$

- The power is an increasing function $\delta$ 
- The power depends on the true values of the treatment means $\mu_i$, the error variance $\sigma^2$, and sample size $n_i$.
- If the experimenter has some prior idea about the treatment means and error variance the sample size (number of replications) that will guarantee a pre-assigned power of the test.
- The degrees of freedom used in the power function are $k-1$ for the numerator degrees of freedom ($k$ is the number of groups) and $N-k$ for the denominator degrees of freedom, where $N = n_ik$ ($n_i$ is the total number of observations in group $i$) the total number of observations in all the groups.  

#### Example

Suppose that an investigator would like to replicate the blood coagulation study with only 3 animals per diet.  In this case $k = 4, n_i = 3.$  The treatment means from the initial study are:

Diet | A | B  | C | D 
-----|---|---|---|---
Average | 61 | 66 | 68| 61|


```r
anova(lm.diets)
```

```
Analysis of Variance Table

Response: y
          Df Sum Sq Mean Sq F value    Pr(>F)    
diets      3    228    76.0  13.571 4.658e-05 ***
Residuals 20    112     5.6                      
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```

So, we will use $\mu_1=$ 61, $\mu_2=$ 66, $\mu_3=$ 68, $\mu_4=$ 61.  The error variance $\sigma^2$ was estimated as $MS_E = 5.6$.  Assuming that the estimated values are the true values of the parameters, the non-centrality parameter of the $F$ distribution is

$$\delta = 3 \times \left((61-64)^2+(66-64)^2+(68-64)^2+(61-64)^2\right)/5.6 = 20.35714$$

This was calculated using R


```r
(3*((61-64)^2+(66-64)^2+(68-64)^2+(61-64)^2))/5.6
```

```
[1] 20.35714
```

If we choose $\alpha = 0.05$ as the significance level then $F_{3,8,0.05}=$ 4.0661806. The power of the test is then 

$$P\left(F_{3,8}(20.36) > 4.07 \right)=0.85.$$

This was calculated using the CDF for the $F$ distribution in R `pf()`.


```r
1-pf(q = 4.07,df1 = 3,df2 = 8,ncp = 20.36)
```

```
[1] 0.8496248
```


### Calculating Power and Sample Size using the `pwr` library in R

There are several libraries in R which can calculate power and sample size for statistical tests.  The library `pwr()` has a function 

`pwr.anova.test(k = NULL, n = NULL, f = NULL, sig.level = 0.05, power = NULL)` 

for computing power and sample size.

- `k`	Number of groups
- `n`	Number of observations (per group)
- `f` Effect size

The effect size is the standard deviation of the population means divided by the common within-population standard deviation. 

$$f = \sqrt{\frac{\sum_{i = 1}^k\left(\mu_i-{\bar \mu} \right)^2/k}{\sigma^2}}.$$

${\bar \mu}=\sum_{i = 1}^k \mu_i/k$, and $\sigma^2$ is the within group error variance.

The relationship between effect size $f$ for ANOVA and the non-centrality parameter $\delta$ is

$$\delta = kn_if^2,$$

where $n_i$ is the number of observations in group $i = 1,...,k$.


```r
eff.size <- sqrt(((61-64)^2+(66-64)^2+(68-64)^2+(61-64)^2)/4/5.6)
library(pwr)
pwr.anova.test(k = 4,n = 3,f = eff.size)
```

```

     Balanced one-way analysis of variance power calculation 

              k = 4
              n = 3
              f = 1.30247
      sig.level = 0.05
          power = 0.8499001

NOTE: n is number in each group
```

Recall that 1.3 is a very large effect size. A plot of effect size versus power when $k = 4,n = 3$ is shown below.


```r
library(pwr)
x <- seq(.05,5,by = 0.01)
plot(x,pwr.anova.test(k = 4,n = 3,f = x)$power,type = "l",xlab = "Effect Size",ylab = "Power",main = "Power vs. Effect Size for k = 4, n = 3")
```

<img src="07-anova_files/figure-html/unnamed-chunk-39-1.png" width="672" />

The plot shows that power is an increasing function of effect size.  The power is 1 for effect sizes at least 1.9. 

### Calculating Power using using Simulation

The power of an ANOVA design can be simulated using R.  

The general procedure for simulating power is:

1. Use the underlying model to generate random data with (a) specified sample sizes, (b) parameter values that one is trying to detect with the hypothesis test, and (c) nuisance parameters such as variances.

2. Run the estimation program (e.g., `t.test()`,`lm()` ) on these randomly generated data.

3. Calculate the test statistic and p-value. 

4. Do Steps 1–3 many times, say, N, and save the p-values.  The estimated power for a level alpha test is the proportion of observations (out of N) for which the p-value is less than alpha.

One of the advantages of calculating power via simulation is that we can investigate what happens to power if, say, some of the assumptions behind one-way ANOVA are violated.

A simple R program that implements 1-4 above, for three treatment groups, is given below.


```r
#Simulate power of ANOVA for three groups

NSIM <- 10000 # number of simulations
res <- numeric(NSIM) # store p-values in res

mu1 <- 2; mu2 <- 2.5;mu3 <- 2  # true mean values of treatment groups
sigma1 <- 1; sigma2 <- 1; sigma3 <- 1 #variances in each group
n1 <- 40; n2 <- 40; n3 <- 40 #sample size in each group

for (i in 1:NSIM) # do the calculations below N times
  { 
y1 <- rnorm(n = n1,mean = mu1,sd = sigma1) # generate a random sample of size n1 from N(mu1,sigma1^2)
y2 <- rnorm(n = n2,mean = mu2,sd = sigma2) # generate a random sample of size n2 from N(mu2,sigma2^2)
y3 <- rnorm(n = n3,mean = mu3,sd = sigma3) # generate a random sample of size n3 from N(mu3,sigma3^2)
y <- c(y1,y2,y3) # store all the values from the groups
trt <- as.factor(c(rep(1,n1),rep(2,n2),rep(3,n3))) # generate the treatment assignment for each group
m <- lm(y~trt) # calculate the ANOVA
res[i] <- anova(m)[1,5] # p-value of F test
}
sum(res<=0.05)/NSIM # calculate p-value
```

```
[1] 0.6188
```


We can check to make sure that our program works by verifying two scenarios where we know the answers. 

(1) Calculate the power of the test when $\mu_1 = 2,\mu_2 = 2.5,\mu_3 = 2, \sigma = 1, n_1 = n_2 = n_3 = 40$, and 

$$f = \sqrt{\frac{\sum_{i = 1}^3\left(\mu_i-{2.17} \right)^2/3}{1^2}}=0.2357023,$$

using `pwr.anova.test()`


```r
mug <- sum(mu1,mu2,mu3)/3
mui <- c(mu1,mu2,mu3)
f1 <- sqrt(((1/3)*sum((mui-mug)^2))/sigma1)
pwr.anova.test(k = 3,f = f1,n = 40,sig.level = 0.05)
```

```

     Balanced one-way analysis of variance power calculation 

              k = 3
              n = 40
              f = 0.2357023
      sig.level = 0.05
          power = 0.6207319

NOTE: n is number in each group
```

The simulation program and `pwr.anova.test()` both calculate power equal to 62%.

(2) Calculate the power directly.


```r
k <- 3
n <- 40
delta <- n*sum((mui-mug)^2)/sigma1
qf(p = .95,df1 = 3,df2 = 117)
```

```
[1] 2.682132
```

```r
1-pf(q = qf(p = .95,df1 = k-1,df2 = n*k-k), df1 = k-1,df2 = n*k-k,ncp = delta,lower.tail = T)
```

```
[1] 0.6207319
```

(3) When $\mu_1=\mu_2=\mu3$ (i.e., when $H_0$ is true) the power of the test is $\alpha$.

When $\delta = 0$ 

$$P\left(F_{k-1,N-k}(0) > F_{k-1,N-K,\alpha} \right)=\alpha.$$


```r
#Simulate power of ANOVA for three groups

NSIM <- 10000 # number of simulations
res <- numeric(NSIM) # store p-values in res

mu1 <- 2; mu2 <- 2;mu3 <- 2  # true mean values of treatment groups
sigma1 <- 1; sigma2 <- 1; sigma3 <- 1 #variances in each group
n1 <- 10; n2 <- 10; n3 <- 10 #sample size in each group

for (i in 1:NSIM) # do the calculations below N times
  { 
y1 <- rnorm(n = n1,mean = mu1,sd = sigma1) # generate a random sample of size n1 from N(mu1,sigma1^2)
y2 <- rnorm(n = n2,mean = mu2,sd = sigma2) # generate a random sample of size n2 from N(mu2,sigma2^2)
y3 <- rnorm(n = n3,mean = mu3,sd = sigma3) # generate a random sample of size n3 from N(mu3,sigma3^2)
y <- c(y1,y2,y3) # store all the values from the groups
trt <- as.factor(c(rep(1,n1),rep(2,n2),rep(3,n3))) # generate the treatment assignment for each group
m <- lm(y~trt) # calculate the ANOVA
res[i] <- anova(m)[1,5] # p-value of F test
}
sum(res<=0.05)/NSIM # calculate p-value
```

```
[1] 0.047
```

## Questions

1. Let $\mu_{A}, \mu_{B},\mu_{C},\mu_{D}$ be the mean coagulation times of diets A, B, C, and D respectively. 

(i)  Formulate a null and alternative hypotheses to compare the mean coagulation times between the four diets.

(ii)  What is the test statistic and P-value of the test in part (a)?

(iii)  Is there a significant difference (at the 1% significance level) between at least two of the diets?

(iv)  What are the assumptions behind:

* The ANOVA table calculations.
* The P-value in the ANOVA table.

2. Interpret the parameters in the additive model for ANOVA  $$y_{ti}=\mu+\tau_t+\epsilon_{ti},$$
where, $y_{ti}$ is the $i^{th}$ observation in the $t^{th}$ treatment group, $\mu$ is the overall mean,  and $\tau_t$ is the deviation produced by treatment $t$, and $\epsilon_{ti}$ is the error. 

