[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

The exercise involves exploring the birthweight of firstborn children versus others by calculating the Cohen's d statistic. A secondary question is to compare the outcome to the same calculation for pregnancy length.

I used the author's function ReadFemPreg to read in the NSFG data as well as his defined function to. calculate Cohen's D:

```python
preg = nsfg.ReadFemPreg()
```

```python
def CohenEffectSize(group1, group2):
    """Computes Cohen's effect size for two groups.
    
    group1: Series or DataFrame
    group2: Series or DataFrame
    
    returns: float if the arguments are Series;
             Series if the arguments are DataFrames
    """
    diff = group1.mean() - group2.mean()

    var1 = group1.var()
    var2 = group2.var()
    n1, n2 = len(group1), len(group2)

    pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
    d = diff / np.sqrt(pooled_var)
    return d
```

For this analysis we are interested in live births, so I have selected them in the `live` variable. Next I divide `live` into firstborn and others (`firsts` and `others`) so I can do the comparison. The last step is to compute Cohen's d for pregnancy length and birthweight:

```python
live = preg[preg.outcome == 1]
firsts = live[live.birthord == 1]
others = live[live.birthord != 1]

preg_length = CohenEffectSize(firsts.prglngth, others.prglngth)
birthweight = CohenEffectSize(firsts.totalwgt_lb, others.totalwgt_lb)

print(preg_length, birthweight)
```

The result is 0.029 for `preg_length` and -0.089 for `birthweight`. The result tells me that the difference in means for birthweight is 0.09 standard deviations and for pregnancy length even lower at 0.029 standard deviations. The direction for the birthweight indicates that firstborns on average would be lighter than other babies, but again, the effect is small even though it is larger than the effect on pregnancy length.