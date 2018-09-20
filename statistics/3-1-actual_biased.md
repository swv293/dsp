[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

>Something like the class size paradox appears if you survey children and ask how many children are in their family. Families with many children are more likely to appear in your sample, and families with no children have no chance to be in the sample.

>Use the NSFG respondent variable `numkdhh` to construct the actual distribution for the number of children under 18 in the respondents' households.

>Now compute the biased distribution we would see if we surveyed the children and asked them how many children under 18 (including themselves) are in their household.

>Plot the actual and biased distributions, and compute their means.

_The Problem_

NSFG respondents are men and women who are in the age range of 15 to 44. One of the questions they have been asked is the number of kids under the age of 18 in their household. However if the respondents were kids in the household, what would the distribution look like? 

To begin, I read in the data using the code:

```
resp = nsfg.ReadFemResp()
resp.numkdhh.describe()
```
The summary statistics for the number of kids under the age of 18 per household is as follows.
```
count    7643.000000
mean        1.024205
std         1.188717
min         0.000000
25%         0.000000
50%         1.000000
75%         2.000000
max         5.000000
Name: numkdhh, dtype: float64
```
The Probability Mass Function is calculated using the Pmf function in the thinkstats2 package.

```
kids_pmf = thinkstats2.Pmf(resp.numkdhh)
```

The PMF for the number of kids per household is given in the table below:

Number of kids/household | PMF
--------------|--------------
0|0.466
1|0.214
2|0.196
3|0.087
4|0.025
5|0.011

As it is clear above, about half the respondents have no kids in their households. 

The plot for the distribution above is given below the code for arriving at it using the `thinkplot` package:
```
thinkplot.PrePlot(2, cols=2)
thinkplot.Hist(kids_pmf, label='numkhdd')
thinkplot.Config(xlabel='Number of kids per household', ylabel='PMF')
thinkplot.PrePlot(2)
thinkplot.SubPlot(2)
thinkplot.Pmf(kids_pmf, label='numkhdd')
thinkplot.Config(xlabel='Number of kids per household', ylabel='PMF')
plt.savefig('actualnumberkids.png')
```
![Actual PMF of number of kids](https://github.com/swv293/ThinkStats2/blob/master/code/actualnumberkids.png)

Now if the question of how many are there in every household was posed to the kids instead of the adults, then the distribution would look different. One way to envision this is to multiply the number of kids per household with the respective PMFs. The rationale here being that as the number of kids in the household increases, so does the probability of conting those kids in the study. The numbers are shown in the table below.

Number of kids/household (n) | PMF (p) | n\*p
--------------|--------------|---------------
0|0.466|0
1|0.214|0.214
2|0.196|0.392
3|0.087|0.261
4|0.025|0.100
5|0.011|0.055

However, in this case, the total probability (which should always be 1), changes, as given below:

Sum of n\*p = 1.022

In order to correct it back to a total probability of 1, we have to normalize all the values by a normalization value to correct the PMF.

Normalization factor:0.978

This normalization when applied to the biased PMF yields the following table:

Number of kids/household (n) | PMF (p) | n\*p | Biased PMF
--------------|--------------|---------------|----------------
0|0.466|0|0
1|0.214|0.214|0.209
2|0.196|0.392|0.383
3|0.087|0.261|0.255
4|0.025|0.100|0.098
5|0.011|0.055|0.054

This calculation is carried out by the `BiasPmf` function as shown below:

```
def BiasPmf(pmf, label):
    new_pmf = pmf.Copy(label=label)

    for x, p in pmf.Items():
        new_pmf.Mult(x, x)
        
    new_pmf.Normalize()
    return new_pmf
```
We can then plot both the observed and the actual PMF distribution on the same graph using the code given below.

```
kids_pmf = thinkstats2.Pmf(resp.numkdhh, label ='actual')
bias_kids_pmf = BiasPmf(kids_pmf, label='observed')
thinkplot.PrePlot(2)
thinkplot.Pmfs([kids_pmf, bias_kids_pmf])
thinkplot.Config(xlabel='Number of kids per household', ylabel='PMF')
```
![BiasedPMF](https://github.com/swv293/ThinkStats2/blob/master/code/bias.png)

Mean of actual distribution: 1.024

Mean of biased distribution: 2.403

While the mean of the actual distribution is 1.024, that of the biased distribution shifts right to 2.403, which gives the impression that on an average each household as at least 2 kids, whereas that is simply not true.

We can then conclude that it is necessary to devise a study that does not introduce unnecessary bias that will ultimately result in erroneous conclusions.
