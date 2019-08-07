# Split-Plot Designs

These designs were originally developed for agriculture by R.A. Fisher and F. Yates.  Due to their applicability outside agriculture they could also be called split-unit designs.



The results from a split-plot experiment are shown in the table below (@bhh2005).  The experiment was designed to study the corrosion resistance of steel bars treated with four different coatings $C_1, C_2, C_3, C_4$ at three duplicated furnace temperatures 360, 370, 380.  The positions of the coated steel bars in the furnace were randomized within each heat. In run 1 the heat was 360 and the first position in the furnace had a steel bar with coating 2 the second position had coating 3 , the third position had coating 1, and the fourth position had coating 4.  But, because the furnace heat was hard to change the heats were run in the systematic order shown.  

The primary interest were the comparison of coatings and how they interacted with temperature.



run   heats   coating    position   replication   resistance
----  ------  --------  ---------  ------------  -----------
r1    T360    C2                1             1           73
r1    T360    C3                2             1           83
r1    T360    C1                3             1           67
r1    T360    C4                4             1           89
r2    T370    C1                1             1           65
r2    T370    C3                2             1           87
r2    T370    C4                3             1           86
r2    T370    C2                4             1           91
r3    T380    C3                1             1          147
r3    T380    C1                2             1          155
r3    T380    C2                3             1          127
r3    T380    C4                4             1          212
r4    T380    C4                1             2          153
r4    T380    C3                2             2           90
r4    T380    C2                3             2          100
r4    T380    C1                4             2          108
r5    T370    C4                1             2          150
r5    T370    C1                2             2          140
r5    T370    C3                3             2          121
r5    T370    C2                4             2          142
r6    T360    C1                1             2           33
r6    T360    C4                2             2           54
r6    T360    C2                3             2            8
r6    T360    C3                4             2           46

The split-plot experiment of corrosion resistance is shown for the first replicate at 360. 

\includegraphics[width = 0.80\textwidth]{../2016/classnotes/week11/furnace.001.jpeg}


The average resistance for each coating and temperature is shown in the table below.


run   heats    average
----  ------  --------
r1    T360       78.00
r2    T370       82.25
r3    T380      160.25
r4    T380      112.75
r5    T370      138.25
r6    T360       35.25



heats    average
------  --------
T360      56.625
T370     110.250
T380     136.500



coating      average
--------  ----------
C1          94.66667
C2          90.16667
C3          95.66667
C4         124.00000

The primary interest was to compare coatings and how they interact with temperature.
How does the split-plot design compare with, say, a 3x4 factorial design of coating and temperature? In the factorial design an oven temperature-coating combination would be randomly  selected then we would obtain a corrosion resistance measure. Then randomly select another oven temperature-coating combination and obtain another corrosion resistance measure until we have a resistance measure for all 12 oven temperature-coating combinations.  To run each combination in random order would require adjusting the furnace temperature up to 24 times (since there were two replicates) and would have resulted in a much larger variance.  The split plot is like a randomized block design (with whole plots as blocks) in which the opportunity is taken to introduce additional factors between blocks. In this design there is only one source of error influencing the resistance.

There are two different experimental units: 

- The six different furnace heats, called whole plots. 
- The four positions within each furnace heat, called subplots, where the differently coated bars could be placed in the furnace. 

There are two different variances associated with the whole plots and subplots.  $\sigma^2_W$ for whole plots and $\sigma^2_S$ for subplots. It would be misleading to treat as if only one error source and one variance.

Achieving and maintaining a given temperature in this furnace was very imprecise.  The whole plot variance, measuring variation from one heat to another, was expected to be large.  

The subplot variance measuring variation from position to position, within a given heat, was expected to be small. 

The subplot effects and subplot-main plot interaction are estimated using with the same subplot error.


Two considerations important in choosing an experimental design are feasibility and efficiency. In industrial experimentation a split-plot design is often convenient and the only practical possibility. This is the case whenever there are certain factors that are *difficult to change* and others that are *easy to change*. In this example changing the *furnace temperature was difficult to change*; rearranging the *positions of the coated bars in the furnace was easy to change*.   


## ANOVA table for split plot experiment

The numerical calculations for the ANOVA of a split-plot design are the same as for other balanced designs (designs where all treatment combinations have the same number of observations) and can be performed in R or with other statistical software. Experimenters sometimes have difficulty identifying appropriate error terms.



```r
spfurcoat1 <- aov(resistance ~ replication * heats * coating, data = tab0901)
summary(spfurcoat1)
```

```
                          Df Sum Sq Mean Sq
replication                1    782     782
heats                      2  26519   13260
coating                    3   4289    1430
replication:heats          2  13658    6829
replication:coating        3    254      85
heats:coating              6   3270     545
replication:heats:coating  6    867     144
```

The whole plot effects are `replication` and `replication:heats`.  So the ANOVA table for the whole plots is:


Source                         DF   SS    MS
----------------------------   --   ---   ---
replication                     1   782   782
replication $\times$ heats      2   13658 6829

The whole plot mean square error is 6829.  This measures the differences between the replicated heats at the three different temperatures.

The subplot effects are:

Source                         DF   SS    MS
----------------------------   --   ---   ---
coating                         3   4289  1430
coating $\times$ heats          6   3270  545

The subplot mean square error is $(254+867)/(3+6)=$ 124.6.  The sum of squares for the subplot error is the sum of interaction between replicate and coating (`replication:coating`) and the three way interaction of replication, heats and coating (`replication:heats:coating`).  The subplot error measures to what extent the coatings give dissimilar results within each of the replicated temperatures. 

In R the ANOVA table for whole plot and sub plot effects can obtained by specifying the subplot error structure explicit using `Error()`.


```r
spfurcoat <- aov(resistance ~ replication + heats + 
                   replication:heats + coating + 
                   heats:coating + Error(heats/replication),
                 data = tab0901)
summary(spfurcoat)
```

```

Error: heats
      Df Sum Sq Mean Sq
heats  2  26519   13260

Error: heats:replication
                  Df Sum Sq Mean Sq
replication        1    782     782
replication:heats  2  13658    6829

Error: Within
              Df Sum Sq Mean Sq F value  Pr(>F)   
coating        3   4289  1429.7  11.480 0.00198 **
heats:coating  6   3270   545.0   4.376 0.02407 * 
Residuals      9   1121   124.5                   
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```


The whole plot effects are under the heading `Error: heats:replication` and the subplot effects are under the heading `Error: Within`.  Under the heading `Error: heats` is mean square error for a one-way ANOVA model comparing heats.


```r
summary( aov(resistance~heats,tab0901))
```

```
            Df Sum Sq Mean Sq F value   Pr(>F)    
heats        2  26519   13260   12.04 0.000328 ***
Residuals   21  23119    1101                     
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```

The ratio of mean square errors follows an $F_{2,2}$. The F statistic for whole plots is 13260/6829= 1.94.  So the p-value to test $H_0:\mu_{360}=\mu_{370}=\mu_{380}$ is 


```r
1-pf(q = 13260/6829,df1 = 2,df2 = 2)
```

```
[1] 0.3399373
```

The subplot effects of coating and the interaction of temperature and coating can be tested by forming F statistics using the subplot mean square error.  These tests are given in the ANOVA table under the heading `Error: Within`.  There are statistically significant differences between coatings and the interaction between temperature and coating.  

The whole plot error mean square 4813 is an estimate of $4\sigma^2_W+\sigma^2_S$. So,

$$4813 = 4\hat {\sigma}^2_W+\hat {\sigma}^2_S.$$

The subplot mean square error is 125 so $\hat {\sigma}^2_S = 125$.  Estimates of the whole plot and sub plot standard deviations are,

$$ \hat {\sigma}_W =\sqrt{\left(\frac{4813-125}{4} \right)}=34.2, \hspace{1cm} \hat {\sigma}_S=\sqrt{125}=11.1.$$

The estimated standard deviation of furnace heats is approximately three times as large as the standard deviation for coatings.

The values for the split plot experiment can be put into one ANOVA table.


Source                         DF   SS    MS      F                P
----------------------------   --   ---   ---    ------------    -----
**Whole plot:**
replication                     1   782   782    782/6829 = 0.12    0.77
heats                           2   26519 13260  13260/6829 = 1.9   0.34
replication $\times$ heats      2   13658 6829
(whole plot error)
**Subplot:**
coating                         3   4289  1430   11.48            0.002
coating $\times$ heats          6   3270  545    4.376            0.02
Subplot error                   9   1121  124.5


Suppose that a split plot experiment is conducted with whole factor plot $A$ with $I$ levels and sub plot factor $B$ with $J$ levels.  The experiment is replicated $n$ times.  The ANOVA table is:

Source                         DF           SS    
----------------------------  ----------   -------------
**Whole plot:**
replication                   $n-1$         $SS_{Rep}$
A                             $I-1$         $SS_A$
replication $\times$ A        $(n-1)(I-1)$  $SS_{W}$
(whole plot error)
**Subplot:**
B                             $J-1$         $SS_B$
$A \times B$                  $(I-1)(J-1)$  $SS_{A \times B}$
Subplot error                 $I(J-1)(n-1)$ $SS_S$

## Split plot ANOVA - How not to do it

Suppose that you didn’t know about the split-plot structure. So the experimenter analyzes the data as a two-way ANOVA.  Would you reach the same conclusions?


```r
furcoatanova <- aov(resistance~heats*coating,data = tab0901)
summary(furcoatanova)
```

```
              Df Sum Sq Mean Sq F value  Pr(>F)   
heats          2  26519   13260  10.226 0.00256 **
coating        3   4289    1430   1.103 0.38602   
heats:coating  6   3270     545   0.420 0.85180   
Residuals     12  15560    1297                   
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```


The two-way ANOVA shows that there is no evidence of a difference in the four coatings, evidence of a difference between temperatures, and no evidence of an interaction between temperature and coating.

What happened?

The two factors temperature and coating use different randomization schemes and the number of replicates is different for each factor. The subplot factor, coatings, restricted randomization to the four positions within a given temperature (whole plot). For the whole plot factor, complete randomization can usually be applied in assigning the levels of A to the whole plots (although this was not the case for the corrosion study).  Therefore, the error should consist of two parts: whole plot error and subplot error.  In order to test the significance of the whole plot factor and the subplot factor we need respective mean squares with the respective whole plot error component and subplot error component respectively. 

The (incorrect) two-way ANOVA model is 

$$y_{ijk}=\eta+\alpha_i+\beta_j+(\alpha\beta)_{ij}+\epsilon_{ijk}, \thinspace \epsilon_{ijk} \sim N(0,\sigma^2)$$

$y_{ijk}$ is the observation for the $k$th replicate of the $i$th level of factor $A$ and the $j$th level of factor $B$. (adapted from Wu and Hamada)




## Split plot ANOVA - How to do it

The correct model is

$$y_{ijk}=\eta+\tau_k+ \alpha_i+ (\tau\alpha)_{ki}+ \beta_j+(\alpha\beta)_{ij}+(\tau\beta)_{kj}+(\tau\alpha\beta)_{kij}+ \epsilon^{\prime}_{ijk}, \thinspace \epsilon^{\prime}_{ijk} \sim N(0,\sigma^2)$$

$i = 1,...,I; \thinspace j = 1,...,J; \thinspace k = 1,...,n.$

- $y_{ijk}$ is the observation for the $k$th replicate of the $i$th level of factor $A$ and the $j$th level of factor $B$. (adapted from Wu and Hamada)

*Whole plot effects*

- $\tau_k$ is the effect of the $k$th replicate.

- $\alpha_i$ is the $i$th main effect for $A$

- $(\tau\alpha)_{ki}$ is the $(k,i)$th interaction effect between replicate and $A$.  This is the whole plot error term.

*Subplot effects*

- $\beta_j$ is the $j$th main effect of $B$

- $(\alpha\beta)_{ij}$ is the $(i,j)$th interaction between $A$ and $B$.

- $(\tau\beta)_{kj}$ is the $(k,j)$th interaction between the replicate and $B$.

- $(\tau\alpha\beta)_{kij}$ is the $(k,i,j)$th interaction between the replicate, $A$, and $B$.

- $\epsilon^{\prime}_{ijk}$ is the error term.

The term $\epsilon_{kij}=(\tau\beta)_{kj}+(\tau\alpha\beta)_{kij}+\epsilon^{\prime}_{ijk}$  is the subplot error term.  

The subplot error is usually smaller than the whole plot error since subplots tend to be more homogeneous than whole plots.  Subplot treatments can be compared with higher precision.
Therefore, factors of greater importance/interest should be assigned to subplots if possible.

## So, what is a split plot?

A split-plot can be thought of as a blocked experiment where the blocks themselves serve as experimental units for a subset of the factors.

Blocks = Whole plots 

Experimental units within blocks = split plots

Corresponding to two levels of experimental units are two levels of randomization.  One randomization to to determine assignment to whole plots.  A randomization of treatments to split-plot experimental units occurs within each plot. 

### Randomizing a Split Plot experiment

The three steps in randomizing a basic split-plot experiment consisting of 5 blocks (replicates), 4 levels of whole plot factor A, and 8 levels of split-plot factor B are:

1. Division of experimental area or material into five blocks.

\includegraphics[width = 0.80\textwidth]{../2016/classnotes/week11/splitplotfig1.jpg}

2. Randomization of four levels of whole plot factor A to each of the five blocks. 

\includegraphics[width = 0.80\textwidth]{../2016/classnotes/week11/splitplotfig2.jpg}

3. Randomization of eight levels of split plot factor B within each level of whole plot factor A. 

\includegraphics[width = 0.80\textwidth]{../2016/classnotes/week11/splitplotfig3.jpg}


## Questions

1. When is a split-plot design appropriate and useful?

2. In a split-plot design is it appropriate that the whole plot factor and sub-plot (or split-plot factor) use the same randomization scheme?  Explain using an example.

