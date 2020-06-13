[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

To explore the impact of bias and the class size paradox, the exercize asks to use the NSFG respondent variable `numkdhh` to construct the actual distribution for the number of children under 18 in the respondents' households, then compare the actual to the biased distribution to see the impact.

I used the author's `BiasPmf` function to do this exercise:

```python
def BiasPmf(pmf, label):
    new_pmf = pmf.Copy(label=label)

    for x, p in pmf.Items():
        new_pmf.Mult(x, x)
        
    new_pmf.Normalize()
    return new_pmf
```

First I read the data, again using the author's function to do so. Next I created a PMF of the actual data in the `numkdhh` column in variable `pmf`. The last step was to call the `BiasPmf` function to create the biased distribution, plot both PMFs and calculate the means:

```python
resp = nsfg.ReadFemResp()

pmf = thinkstats2.Pmf(resp.numkdhh, label='actual')

biased_pmf = BiasPmf(pmf, label='observed')

thinkplot.PrePlot(2)
thinkplot.Pmfs([pmf, biased_pmf])
thinkplot.Config(xlabel='Class size', ylabel='PMF')

print(pmf.Mean(), biased_pmf.Mean())
```

The difference in means is about 1.38 kids per household, so quite large. The difference in PMF is most prominent for households without kids, which makes sense considering that those will not be able to make it into the biased sample.

![Comparison of biased vs actual PMF](/Users/stephan/Data_Science/Metis/bootcamp_prework/dsp/lessons/statistics/Bias.png)

