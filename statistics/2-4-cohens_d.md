[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

> Using the variable ```totalwgt_lb```, investigate whether first babies are lighter or heavier than others. Compute Cohen’s effect size to quantify the difference between the groups. How does it compare to the difference in pregnancy length?

_The Problem_

Allen Downey uses data from the [NSFG](https://www.cdc.gov/nchs/nsfg/nsfg_cycle6.htm) website to answer whether the weights of first born babies differ significantly from that of babies born later (second and onward). The data in itself is a sampling of the population, which uses replies from approximately 7500 female respondents to answer questions regarding fertility of the U.S. population as a whole.

_The Data to answer this question_

First we read in the data from the .dat file containg the outcomes of the pregnancy and its associated data. This is done using the code written by Downey, which combines the details of a Strata dictionary file and the data file to create a dataframe from which we can query the necessary information. This data frame is stored in the ```preg``` variable.

Since we are interested in the live birth weights, Downey selects these rows with pregnancy outcome equal to 1 - the code for live births - into the variable ```live```. 
```
    preg = nsfg.ReadFemPreg()
    live = preg[preg.outcome == 1]
```

We then separate the live births into to categories, firsts - containing the data pertaining to the first born babies - and others, with the remaining data.

```
firsts = live[live.birthord == 1]
others = live[live.birthord != 1]
```
_Analyzing the data_

Next, I wrote the code to pull out the data from the ```totalwgt_lb``` column in to a dict with the frequencies associated with each weight. For this purpose, I used a function Downey wrote in the thinkstats2 package called Hist. Also, to smoothen the data a bit (for better visualization of the histogram) I used ```round``` to round up the numbers. 
```
first_wgt = thinkstats2.Hist(round(firsts.totalwgt_lb), label='first')
other_wgt = thinkstats2.Hist(round(others.totalwgt_lb), label='other')
```

The histogram was plotted and labelled using the package Downey wrote.
 
```
width = 0.7
thinkplot.PrePlot(2)
thinkplot.Hist(first_wgt,  align='right', width=width)
thinkplot.Hist(other_wgt, align='left', width=width)
thinkplot.Config(xlabel='weight in lb', ylabel='Count', xlim=[0, 14])
```
Here are the key takeaways from the distribution.

1. Central tendency: The weights of both the categories cluster around 7 pounds. The birth weight of the others group tends to move right compared to the firsts, suggesting a slight increase in their birth weights. But is this increase significant is what we'd like to answer.
```
a=firsts.totalwgt_lb.mean()
b=others.totalwgt_lb.mean()
print(a-b)
```
The actual difference in the weights is 0.125 lb.

2. Mode: The data is clustered around one spot, so it is not multimodal.

3. Variance: The variance in the data is also pretty similar, with firsts having a variance of 2.0 and others around 1.9.
```
firsts.totalwgt_lb.var(), others.totalwgt_lb.var()
```
4. Outliers: Not many outliers in either groups. Sample code pasted below.
```for weight, freq in first_wgt.Smallest(10):
    print(weight, freq)
```

Finally, in order to glean whether the difference in the means of these two groups is significant or not, I calculated the Cohen's d statistic. What the d statistic checks is whether the difference in the means of the two groups is not a consequence of the differences in their variabilities. It returns a value correcting for the variabilities and the size of each category by calculating a pooled standard deviation.

```
CohenEffectSize(firsts.totalwgt_lb , others.totalwgt_lb)
```
This gives a value of -0.089. Since the means of others was larger than the firsts, it gives rise to the negative d statistic. However, the difference is still pretty small - less than a tenth of a standard deviation. 

The difference in the pregnancy lengths between the two categories was 0.029 towards the firsts. Although the d statistic for birth weights in pounds is larger than that (favoring the others, hence the negative), it still is not significant enough.
