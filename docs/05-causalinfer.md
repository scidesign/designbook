# Causal Inference

## The Fundemental Problem of Causal Inference

The following is adapted from @imbens2015 :

Suppose Bob, at a particular point in time, is contemplating whether or not to take an aspirin for a headache. There are two treatment levels, taking an aspirin, and not taking an aspirin. If Bob takes the aspirin, his headache may be gone, or it may remain, say, an hour later; we denote this outcome, which can be either “Headache” or “No Headache,” by $y^1$. (We could use a finer measure of the status of my headache an hour later, for example, rating my headache on a ten-point scale, but that does not alter the fundamental issues involved here.) Similarly, if Bob does not take the aspirin, his headache may remain an hour later, or it may not; we denote this potential outcome by $y^0$, which also can be either “Headache,” or “No Headache.” There are therefore two potential outcomes, $y^1$ and $y^0$, one for each level of the treatment. The causal effect of the treatment involves the comparison of these two potential outcomes.

Because in this example each potential outcome can take on only two values, the unit- level causal effect – the comparison of these two outcomes for the same unit – involves one of four (two by two) possibilities:

1. Headache gone only with aspirin:
 $y^1$ = No Headache, $y^0$ = Headache
2. No effect of aspirin, with a headache in both cases: 
$y^1$ = Headache, $y^0$ = Headache
3. No effect of aspirin, with the headache gone in both cases: $y^1$ = No Headache, $y^0$ = No Headache
4. Headache gone only without aspirin:
$y^1$ = Headache, $y^0$ = No Headache

There are two important aspects of this definition of a causal effect.



1. The definition of the causal effect depends on the potential outcomes, but it does not depend on which outcome is actually observed. Specifically, whether Bob takes an aspirin (and am therefore unable to observe the state of my headache with no aspirin) or do not take an aspirin (and am thus unable to observe the outcome with an aspirin) does not affect the definition of the causal effect. 



2. The causal effect is the comparison of potential outcomes, for the same unit, at the same moment in time post-treatment. In particular, the causal effect is not defined in terms of comparisons of outcomes at different times, as in a before-and-after comparison of my headache before and after deciding to take or not to take the aspirin. @holland1986 states that “The fundamental problem of causal inference” is therefore the problem that at most one of the potential outcomes can be realized and thus observed. If the action you take is Aspirin, you observe $y^1$ and will never know the value of $y^0$ because you cannot go back in time. Similarly, if your action is No Aspirin, you observe $y^0$ but cannot know the value of $y^1$.  In general, therefore, even though the unit-level causal effect (the comparison of the two potential outcomes) may be well defined, by definition we cannot learn its value from just the single realized potential outcome. 

The outcomes that would be observed under control and treatment conditions are often called **counterfactuals or potential outcomes**.

If Bob took aspirin for his headache then then $y^1$ is observed and $y^0$ is the unobserved counterfactual outcome—it represents what would have happened to Bob if he had no taken aspirin. Conversely, if Bob had not taken aspirin then $y^0$ is observed and $y^1$ is counterfactual. In either case, a simple treatment effect for Bob can be defined as
$$ \mbox{treatment effect for Bob }= y^1-y^0.$$

### Example of the fundemental problem

The table below shows hypothetical data for an experiment with 100 units (200 potential outcomes). The table shows what the data that is required to determine causal effects for each person in the data set—that is, it includes both potential outcomes for each person. Let $y_i^0$ be the potential outcome for unit $i$ when $T_i = 0$ and $y_i^1$ be the potential outcome for unit $i$ when $T_i = 1$.  $X_i$ is a pre-treatment characteristic or covariate for each unit.

-------------------------------------------------------------
Unit     $T_i$  $y_i^0$  $y_i^1$   $y_i^0 -y_i^1$
-------  -----  -------  --------- ---------------
    1     0        **69**     75         -6
    
    2     1       80         **76**      4
    
    3     1       71        **69**       1       
    
   \vdots \vdots \vdots     \vdots      \vdots   
    
  100     0      **81**      78           3
----------------------------------------------------------

The observed data is actually

-------------------------------------------------------------
Unit      $T_i$  $y_i^0$  $y_i^1$   $y_i^0 -y_i^1$
-------   -----  -------  --------- ---------------
    1     0        **69**     ?         ?
    
    2     1       ?         **76**      ?
    
    3     1       ?        **69**       ?       
    
   \vdots \vdots \vdots     \vdots      \vdots
    
  100     0      **81**     ?           ?
----------------------------------------------------------

The fundamental problem of causal inference is that at most one of these two potential outcomes, $y_i^0$ and $y_i^1$, can be observed for each unit $i$. The bottom table displays the data that can actually be observed. The $y_i^1$ values are “missing” for those in the control group and the $y_i^0$ values are “missing” for those in the treatment group. (pg. 170-171, @gelman2006)

We cannot observe both what happens to an individual after taking the treatment (at a particular point in time) and what happens to that same individual after not taking the treatment (at the same point in time). Thus we can never measure a causal effect directly.


## Randomized experiments as a solution to the fundemental problem of causal inference

Randomization and experimentation is one approach to dealing with the fundamental problem of causal inference.  Outcomes are observed on a sample of units to learn about the distribution of outcomes in the population.  The fundamental problem states that we cannot compare treatment and control outcomes for the same units, so we try to compare them on similar units. Similarity can be attained by using randomization to decide which units are assigned to the treatment group and which units are assigned to the control group. 

Other approaches to dealing with the problem is statistical adjustment via regression modelling and finding close substitutes to the units that did not receive treatment (see @gelman2006).

Suppose that in an experiment units are randomly assigned to receive treatment and control, and also that the units are a random sample from a population of interest. The random sampling and random treatment assignment allow us to estimate the average causal effect of the treatment in the population, and regression modeling can be used to refine this estimate.

## Average causal effects and randomized experiments

In this section average causal effects will be described in terms of a control group - a group that does not receive treatment, although the group could have received another treatment instead of no treatment.   

In most practical situations it's impossible to estimate individual-level causal effects but, we can design studies to estimate the population average treatment effect:

$$ \mbox{average treatment effect} = {\bar y}^1-{\bar y}^0,$$

where ${\bar y}^1 = \sum_{i = 1}^{n_1} y_i^1/n_1$ and ${\bar y}^0 = \sum_{i = 1}^{n_0} y_i^0/n_0$.

The control group is a group of units that could have ended up in the treatment group, but due to chance they just happened not to get the treatment. Therefore, on average, their outcomes represent what would have happened to the treated units had they not been treated; similarly, the treatment group outcomes represent what might have happened to the control group had they been treated.

If $n_0$ units are selected at random from the population and given the control, and $n_1$ other units are randomly selected and given the treatment, then the observed sample averages of $y$ for the treated and control units can be used to estimate the corresponding population quantities, ${\bar y}^1$ and ${\bar y}^0$, with their difference estimating the average treatment effect (and with standard error $\sqrt{S^2_0/n_0+S^2_1/n_1}$). This works because the $y_i^0$ for the control group are a random sample of the values in the entire population. Similarly, the $y_i^1$ for the treatment group are a random sample of the $y_i^1$’s in the population.


Equivalently, if we select $n_0 + n_1$ units at random from the population, and then randomly assign $n_0$ of them to the control and $n_1$ to the treatment, we can think of each of the sample groups as representing the corresponding population of control or treated units. Therefore the control group mean can act as a counterfactual for the treatment group (and vice versa).

In medical studies such as clinical trials it is common to select $n_0 + n_1$ units nonrandomly from the population but then the treatment is assigned at random within this sample.  Causal inferences are still justified, but the inferences no longer generalize to the entire population (@gelman2006).

### Stable Unit Treatment Value Assignment

**The assumption.** The potential outcomes for any unit do not vary with the treatments assigned to other units, and, for each unit, there are no different forms or versions of each treatment level, which lead to different potential outcomes.

The stable unit treatment value assumption involves assuming that treatments applied to one unit do not affect the outcome for another unit. For example, if Adam and Oliver are in different locations and have no contact with each other, it would appear reasonable to assume that if Oliver takes an an aspirin for his headache then his behaviour has no effect on the status of Adam's headache. This assumption might not  hold if Adam and Oliver are in the same location, and Adam's behavior, affects Oliver's behaviour.  SUTVA incorporates the idea that Adam and Oliver do not interfere with one another and the idea that for each unit there is only a single version of each treatment level (e.g., there is only one dose of aspirin). [@imbens2015]

The causal effect of aspirin on headaches can be estimated if we are able to exclude the possibility that your taking or not taking aspirin has any effect on my headache, and that that the aspirin tablets available to me are of different strengths. These are assumptions that rely on previously acquired knowledge of the subject matter for their justification. Causal inference is generally impossible without such assumptions, and thus it is critical to be explicit about their content and their justifications. [@imbens2015] 

## Ignorable Assignment Mechanisims

A **covariate** is a pre-treatment characteristic of an experimental unit that is not affected by treatment.  In many studies the age and sex of a subject would be considered a covariate.

The **assignment mechanism** is the process for deciding which units receive treatment and which receive control.

A treatment assignment is **(strongly) ignorable** if: 

(1) the probability of a unit receiving treatment is strictly between zero and one; and 

(2) treatment assignment is independent of potential outcomes conditional on all observed and unobserved covariates. If a treatment assignment is not strongly ignorable then it is said to be non-ignorable

Strongly ignorable treatment assignment can also be expressed in terms of conditional independence. If treatment assignment $T$ is conditionally independent of $y^0, y^1$ given confounding covariates $X$ and $0<P(T = 1|y^0,y^1,X)<1$ then the treatment assignment is said to be **strongly ignorable**. Symbolically this is represented as 

$$y^0,y^1 \bot T | X.$$

This means that the conditional distribution of potential responses is the same across levels of the treatment variable once we condition on the confounding covariates $X$.  

Another way to view ignorability is:

$$P(T = 1|y^0,y^1,X)=P(T = 1|X).$$

If treatments were assigned by the flip of a coin then the coin flips may depend on the covariates but not on the potential responses. 

When the treatment assignment mechanism is random, say, using a coin toss then the assignment mechanism is strongly ignorable.  This is why the treatment effects in randomized experiments can be estimated using a simple difference in means to estimate the average causal effect without conditioning on pre-treatment covariates.  In later chapters we will see how blocking can be used to satisfy the strongly ignorable condition.  


### The Perfect Doctor Example

The following example is adapted from Donald Rubin (add ref.).

- Suppose that a doctor prescribes surgery (labeled 1) or drug (labeled 0) for a certain condition.  
- The doctor knows enough about the potential outcomes of the patients so assigns each patient the treatment that is more beneficial to that patient.

unit         |  $y^0_i$  | $y^1_i$   |$y^1_i - y^0_i$   
-------------|------------|------------|-----------------
patient #1   |    1       |  7         |       6
patient #2   |    6       |  5         |      -1
patient #3   |    1       |  5         |       4
patient #4   |    8       |  7         |      -1
Average      |    4       |  6         |       2

$y$ is years of post-treatment survival. 

- Patients receiving surgery on average live 2 years longer.
- Patients 1 and 3 will receive surgery and patients 2 and 4 will receive drug treatment.
- The observed treatments and outcomes are in this table, where 
$$T_i =
\left\{
	\begin{array}{ll}
		1  & \mbox{if surgery is assigned } \\
		0 & \mbox{if drug is assigned }
	\end{array}
\right.$$

and 

$$y_i^{obs} =
\left\{
	\begin{array}{ll}
		y_i^1  & \mbox{if surgery is assigned } \\
		y_i^0 & \mbox{if drug is assigned }
	\end{array}
\right.$$



unit         |   $T_i$    | $y_i^{obs}$ 
-------------|------------|------------
patient #1   |      1     |  7         
patient #2   |      0     |  6          
patient #3   |      1     |  5         
patient #4   |      0     |  8         
**Average Drug** |            |  **7**
**Average Surg** |            |  **6**

- The observed data tells us that patients receiving drug live, on average, one year longer. 
- This shows that we can reach invalid conclusions if we look at the observed values of potential outcomes without considering how the treatments were assigned.

- In order to study causal effects the probability of a treatment assignment must be strictly between 0 and 1.

- The assignment mechanism depended on the potential outcomes and was therefore nonignorable.

- The observed difference in means is misleading in this situation. The biggest problem when using the difference of sample means in this example is that we have effectively pretended that we had an ignorable treatment assignment when in fact we did not. 

## Questions

1. (Adapted from @gelman2006, Chapter 9) Suppose you are interested in the effect of the presence of vending machines in schools on childhood obesity. What randomized experiment would you want to do (in a perfect world) to evaluate this question?

2.  What is the definition of ignorable treatment assignment?  

(a) Give an example of a study where the treatment assignment is strongly ignorable. 

(b) Give an example of a study where the treatment assignment is non-ignorable. 

3. (Adapted from @gelman2006, Chapter 9) The table below describes a hypothetical experiment on 2400 persons. Each row of the table specifies a category of person, as defined by his or her pre-treatment predictor $x$, treatment indicator $T$ , and potential outcomes $Y(0)$, $Y(1)$. (For simplicity, we assume unrealistically that all the people in this experiment fit into these eight categories.)

Category | persons in category |$x$|$T$| $Y(0)$ | $Y(1)$
---------|---------------------|---|---|--------|------
  1      |  300                | 0 | 0 | 4      | 6
  2      |  300                | 1 | 0 | 4      | 6
  3      |  500                | 0 | 1 | 4      | 6
  4      |  500                | 1 | 1 | 4      | 6
  5      |  200                | 0 | 0 | 10     | 12
  6      |  200                | 1 | 0 | 10     | 12
  7      |  200                | 0 | 1 | 10     | 12
  8      |  200                | 1 | 1 | 10     | 12 

  
In making the table we are assuming omniscience, so that we know both $Y(0)$ and $Y(1)$ for all observations. But the (non omniscient) investigator would only observe $x$, $T$, and $Y(T)$  for each unit. (For example, a person in category 1 would have $x = 0$,$T = 0$,$Y(0)=4$, and a person in category 3 would have $x = 0$,$T = 1$,$Y(1)=6$.)

(a) Give an example of a context for this study.  Define $x, T, Y(0), Y(1)$.

(b) What is the average treatment effect in this population of 2400 persons?

(c) Is it plausible to believe that these data came from a randomized experiment?
Defend your answer.

(d) Another population quantity is the mean of $Y$ for those who received the
treatment minus the mean of $Y$ for those who did not. What is the relation
between this quantity and the average treatment effect?

(e) For these data, is it plausible to believe that treatment assignment is strongly ignorable
given the covariate $x$? Defend your answer.

4. (Adapted from @gelman2006, Chapter 9) An observational study to evaluate the effectiveness of supplementing a reading program 
with a television show was conducted in several schools in grade 4.  Some classroom teachers chose to supplement their reading program with the television show and some teachers chose not to supplement their reading program. Some teachers chose to supplement if they felt that it would help their class improve their reading scores.  The study collected data on a large number of student and teacher covariates measured before the teachers chose to supplement or not supplement their reading program.  The outcome measure of interest is student reading scores. 

(a)  Describe how this study could have been conducted as a randomized experiment.


(b)  Is it plausible to assume that supplementing the reading program is ignorable in this observational study? 

## Answers to Questions

1. Suppose you are interested in the effect of the presence of vending machines in schools on childhood obesity. What randomized experiment would you want to do (in a perfect world) to evaluate this question?

> *One possible design: Design a randomized experiment with vending machines as the treatment and the rate of obesity as the 
> outcome.  Schools would be randomly assigned to have vending machines and no vending machines.  The weight of children in 
> the school would be measured in all schools before the vending machines were installed and at the end of the school year.*

2.  What is the definition of strongly ignorable treatment assignment?  

> See definition above.

> Let $Z=1$ if a unit is treated and $Z=0$ if a unit is control.  Let $Y(0)$ be the potential outcome if the
> unit is treated and $Y(1)$ the potential outcome if the unit is a control, and $X$ be a vector of 
> pretreatment covariates:  $$ P(Z|Y(0),Y(1),X)=P(Z|X),$$

and $0<P(Z|Y(0),Y(1),X)<1$.

(a) Give an example of a study where the treatment assignment is ignorable. 

> *Any study that is a randomized experiment. For example, if two fertilizers are randomly assigned to 12 plots of 
> land with one fertilzer assigned to 6 plots and the other fertilzer assigned to the remaining plots.  The 
> probability of any particlular treatment assignment is ${\binom {12} {6}}^{-1}$.* 

(b) Give an example of a study where the treatment assignment is non-ignorable. 

> *A doctor assigns treatments to patients based on their prior medical history and how successful the doctor 
> feels that the treatment will be for the patient.*

3. (Adapted from Hill and Gelman, Chapter 9) The table below describes a hypothetical experiment on 2400 persons. Each row of the table specifies a category of person, as defined by his or her pre-treatment predictor $x$, treatment indicator $T$ , and potential outcomes $Y(0)$, $Y(1)$. (For simplicity, we assume unrealistically that all the people in this experiment fit into these eight categories.)

Category | persons in category |$x$|$T$| $Y(0)$ | $Y(1)$
---------|---------------------|---|---|--------|------
  1      |  300                | 0 | 0 | 4      | 6
  2      |  300                | 1 | 0 | 4      | 6
  3      |  500                | 0 | 1 | 4      | 6
  4      |  500                | 1 | 1 | 4      | 6
  5      |  200                | 0 | 0 | 10     | 12
  6      |  200                | 1 | 0 | 10     | 12
  7      |  200                | 0 | 1 | 10     | 12
  8      |  200                | 1 | 1 | 10     | 12 

In making the table we are assuming omniscience, so that we know both $Y(0)$ and $Y(1)$ for all observations. But the (nonomniscient) investigator would only observe $x$, $T$, and $Y(T)$  for each unit. (For example, a person in category 1 would have $x=0$,$T=0$,$Y(0)=4$, and a person in category 3 would have $x=0$,$T=1$,$Y(1)=6$.)

(a)  Give an example of a context for this study.  Define $x, T, Y(0), Y(1)$.

> Let $T=0$ if subjects receive aspirin and $T=1$ if subjects receive tylenol and aspirin. $x=0$ if the subject
> is male and $x=1$ if the subject is female.  $Y(0)$ is the time to pain relief if the subject received aspirin
> and $Y(1)$ is the time to pain relief if the subject received tylenol and aspirin.  
>
> In reality we can't observe both responses and the response that we observe will be $Y^{obs}=Z*Y(1)+(1-Z)*Y(0)$.
> But to illustrate the concepts we will assume that we can observe both $Y(0)$ and $Y(1)$.

(b) What is the average treatment effect in this population of 2400 persons?

> $${\bar Y(0)}=\frac{300\times4+300\times4+500\times4+500\times4+200\times10+200\times10+200\times10+200\times10}{300+300+500
> +500+200+200+200+200} = 6$$
>
> $${\bar Y(1)}=\frac{300\times6+300\times6+500\times6+500\times6+200\times12+200\times12+200\times12+200\times12}{300+300+500
> +500+200+200+200+200} = 8$$
>
> The average treatment effect is ${\bar Y(0)}-{\bar Y(1)}=6-8=-2$.

(c) Is it plausible to believe that these data came from a randomized experiment?
Defend your answer.

> *500/1000 (50\%) subjects in the $T=0$ have $x=0$ 
> and 700/1400 (50\%) subjects in the $T=1$ group have $x=0$. If the data came from a randomized experiment we would expect that 
> all the observed covariates would be balanced.  Therefore it seems plausible that the data came from a randomized 
> experiment. * 

(d) Another population quantity is the mean of $Y$ for those who received the
treatment minus the mean of $Y$ for those who did not. What is the relation
between this quantity and the average treatment effect?

> The average for those that received $T=0$:
>
> $$ \frac {300\times4+300\times4+200\times10+200\times10}{300+300+200+200}=6.4$$
>
>The average for those that received $T=0$:
> $$ \frac {500\times6+500\times6+200\times12+200\times12}{500+500+200+200}=7.7$$
>
> *The treatment effect using these averages is 7.7-6.4=+1.3.  The relation between this quantity and the average treatment
> effect is that this quantity is based on the observed responses.  The average treatment effect is
> based on the observed and unobserved responses.
> This quantity yields a different treatment effect compared to the average treatment effect.*

(e) For these data, is it plausible to believe that treatment assignment is strongly ignorable
given the covariate $x$? Defend your answer.

> If treatment assignment is strongly ignorable then $P(T|Y(0)=y_0,Y(1)=y_1,X=x)=P(T|X=x).$  So, let's consider the case where $y_0=4$ and, 
> $y_1=6$.  $$P(T|Y(0)=4,Y(1)=6,X=0)=\frac{300}{300+500}=\frac{3}{8},$$ and $$P(T=0|X=0)=\frac{300+200}{300+500+200+200}=\frac {5}{12}.$$
> Therefore, $$P(T|Y(0)=4,Y(1)=6,X=0) \ne P(T=0|X=0).$$  This means that the treatment assignment is non-ignorable since treatment
> assignment is not (conditionally) independent of the potential outcomes given the covariate.

4. An observational study to evaluate the effectivness of supplementing a reading program 
with a television show was conducted in several schools in grade 4.  Some classroom teachers chose to supplement their reading program with the television show and some teachers chose not to supplement their reading program. Some teachers chose to supplement if they felt that it would help their class improve their reading scores.  The study collected data on a large number of student and teacher covariates measured before the teachers chose to supplement or not supplement their reading program.  The outcome measure of interest is student reading scores. 

(a) Describe how this study could have been conducted as a randomized experiment.

> Classrooms could be randomly assigned to supplement their reading programs or not supplement their reading programs instead of teachers
> choosing to supplemnt or not supplemnt their reading programs.


(b)  Is it plausible to assume that supplementing the reading program is ignorable in this observational study? 

> No, since teachers intentionally choose to supplement or not supplement based on the characteristics of their class and how 
> they feel that the class will respond to the reading supplement.  In other words treatment assignment is
> dependent on the potential outcomes given pre-treatment covariates.



