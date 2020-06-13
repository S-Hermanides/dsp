[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

This exercise asks us to use the distribution in height from the chapter (BRFSS data) to find out how much of the U.S. male population qualifies for the casting requirements of the Blue Man Group.

The distribution has `mu` of 178 cm. and `sigma` of 7.7 cm. First step is to use `spicy.stats.norm` to create a distribution object. Then I had to convert the heights into cm. The CDF for this distribution shows the probability of being a certain height or less, so the difference between the upper and lower bound shows the probability of being between the upper and lower bounds. 34.3% of the U.S. male population is in the range between 5'10'' and 6'1''.

```python
mu = 178
sigma = 7.7
dist = scipy.stats.norm(loc=mu, scale=sigma)

def convert_height(feet, inches):
    feet_conv = 30.48
    inch_conv = 2.54
    return (feet * feet_conv) + (inches*inch_conv)

lower = convert_height(5,10)
upper = convert_height(6,1)

perc_below_lower = dist.cdf(lower)
perc_below_upper = dist.cdf(upper)
blue_man_height = perc_below_upper - perc_below_lower
print(perc_below_lower, perc_below_upper, blue_man_height)
```

For the output see Capter5_ex1.ipynb