[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

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


```python
firsts['totalwgt_lb'].mean(), others['totalwgt_lb'].mean()
```




    (7.201094430437772, 7.325855614973262)




```python
CohenEffectSize(firsts['totalwgt_lb'], others['totalwgt_lb'])
```




    -0.088672927072602



The difference in mean birth weights is .09 standard deviations, with non-first babies being slightly heavier (7.33 lbs vs 7.20 lbs). This effect is 3x as large as the difference in pregnancy length (length d = .03), with first babies, on average, born later than non-first babies. First babies appear to be born later and weigh less, but Cohen's d's of .03 and .09, respectively, are far from large effects. 
