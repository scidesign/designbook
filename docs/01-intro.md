# Introduction 

## Why Design Scientific Studies?

Why should scientific studies be designed? Some reasons include avoiding bias, variance reduction, and system optimization.   

## Big Data and Designing Scientific Studies

### What is Big data and why does it matter?


Big data is often thought to lead to more accurate information.  Designing scientific studies can lead to the collection of high quality data which in turn leads to more accurate information compared to having a large amount of data that is lower quality.

### Is statistical sampling and randomization still relevant in the era of Big Data?

This question was asked by Professor Xiao-Li Meng [asks](http://statistics.fas.harvard.edu/news/xiao-li-meng-chicago-statistician-year).  

Meng then considers the following: if we want to estimate a population mean which data set would give us more accurate results: a 1% simple random sample or a data set containing self-reports of the quantity of interest that covers 95% of the population?

The total error is captured by the mean square error ($MSE$). The mean square error of an estimator $\hat \theta$ of $\theta$ is,

$$MSE = E\left({\hat \theta}-\theta\right)=Var\left({\hat \theta}\right)+\left(E\left({\hat \theta}-\theta\right)\right)^2.$$


In other words, $Total \thinspace Error = Variance + Bias^2$. The term $E\left({\hat \theta}-\theta\right)$ is called the bias of the estimator $\hat \theta$. If the bias is 0 then the estimator is called unbiased.  

Suppose we have a finite population of measurements $\{x_1,..., x_N\}$ of some quantity, say the total number of hours spent on the internet during a one-year period for every person in Canada.  In 2015 the [population of Canada](http://www.statcan.gc.ca/daily-quotidien/150617/dq150617c-eng.htm) is $N = 35,749,600$ or approximately 35.8 Million people.  In order to estimate the mean number of hours spent on the Internet is it better to: take a simple random sample of 100 people and estimate the mean number of hours spent on the Internet; or use a large  database (much larger than the random sample) that contains self-reports of hours spent on the Internet?

Suppose that $\bar{x}_a$ is the sample mean from the database and $\bar{x}_s$ is the mean from the random sample.  [Meng](http://www.stat.harvard.edu/Faculty_Content/meng/COPSS_50.pdf) shows that in order for $MSE\left(\bar{x}_a\right) < MSE\left(\bar{x}_s\right)$ it's sufficient that

$$ f_a > \frac{n_s\rho_N^2}{1+n_s\rho^2},$$

where $f_a$ is the fraction of the population in the database, $\rho$ is the correlation between the response being recorded and the recorded value, and $n_s$ is the size of the random sample.  For example, if $n_s = 100$ the database would need over 96% of the population if $\rho = 0.5$ to guarantee that $MSE\left(\bar{x}_a\right) < MSE\left(\bar{x}_s\right)$.  In our example this would require a database with 34,319,616 Canadians. 

This illustrates the main advantage of probabilistic sampling and the danger of putting faith in "Big Data" simply because it's Big! 
