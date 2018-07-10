[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

>Something like the class size paradox appears if you survey children and ask how many children are in their family. Families with many children are more likely to appear in your sample, and families with no children have no chance to be in the sample.

>Use the NSFG respondent variable `numkdhh` to construct the actual distribution for the number of children under 18 in the respondents' households.

>Now compute the biased distribution we would see if we surveyed the children and asked them how many children under 18 (including themselves) are in their household.

>Plot the actual and biased distributions, and compute their means.

_The Problem_

NSFG respondents are men and women who are in the age range of 15 to 44. One of the questions they have been asked is the number of kids under the age of 18 in their household. However if the respondents were kids in the household, what would the distribution look like? 


kids_pmf:

Number of kids/household | PMF
--------------|--------------
0|0.466
1|0.214
2|0.196
3|0.087
4|0.025
5|0.011



Number of kids/household (n) | PMF (p) | n\*p
--------------|--------------|---------------
0|0.466|0
1|0.214|0.214
2|0.196|0.392
3|0.087|0.261
4|0.025|0.100
5|0.011|0.055


Sum of n\*p = 1.022

Normalization factor:0.978


Number of kids/household (n) | PMF (p) | n\*p | Biased PMF
--------------|--------------|---------------|----------------
0|0.466|0|0
1|0.214|0.214|0.209
2|0.196|0.392|0.383
3|0.087|0.261|0.255
4|0.025|0.100|0.098
5|0.011|0.055|0.054

Mean of actual distribution: 1.024
Mean of biased distribution: 2.403

