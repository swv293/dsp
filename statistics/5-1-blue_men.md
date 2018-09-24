[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

>> **Exercise**: In the BRFSS (see Section 5.4), the distribution of heights is roughly normal with parameters µ = 178 cm and σ = 7.7 cm for men, and µ = 163 cm and σ = 7.3 cm for women.

>> In order to join Blue Man Group, you have to be male between 5’10” and 6’1” (see http://bluemancasting.com). What percentage of the U.S. male population is in this range? Hint: use scipy.stats.norm.cdf.

>> scipy.stats contains objects that represent analytic distributions

As suggested by the problem, I have used the scipy.stats package to generate a normal distribution with the parameters μ and
σ for the distribution of heights of men in the US population.
```
import scipy.stats
mu = 178
sigma = 7.7
dist = scipy.stats.norm(loc=mu, scale=sigma)
```
Next based on this normal distribution, I calculate the CDF for the a male of height 5'10" (= 177.8 cm) and below and the CDF for a male of height 6'1" (= 185.42 cm) and below.
```
a=dist.cdf(177.8)
b=dist.cdf(185.42)
```
The value for a is 0.48963902786483265 and that for b is 0.8323858654963063, meaning that about 48.9% of the US male population is below 177.8 cm and 83.2% of the US male population is below 185.42 cm.

Therefore the percent of the US population that is eligible for joining the blue man group is given by the code:

```
percent = (b-a)*100
print(percent)
```

This returns an answer of 34.274683763147365. Therefore, about 34.3% of the US male population is eligible for joining the Blue Man group.

This answer makes sense as the mean for the us population is 178 cm, which is very close to 177.8 cm - the lower limit of the height requirement of the Blue Man group. Now, the upper limit of 185.42 cm - is close to + 1 σ from the mean (178 + 7.7 = 185.7 cm). Now, in a normal distribution about 68.26% of values lie  within 1σ, which divides to 34.13% on either side of the mean. Given the height requirement of the Blue Man Group, these values match well with one another!
