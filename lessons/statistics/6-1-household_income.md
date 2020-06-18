[Think Stats Chapter 6 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2007.html#toc60) (household income)

```python
Median(sample), Mean(sample)
```




    (10000.0, 34330.52510748183)




```python
Skewness(sample), PearsonMedianSkewness(sample)
```




    (6.775200881176056, 0.9595638278153094)




```python
cdf.Prob(Mean(sample))
```




    0.7923451305753809



79% of households report a taxable income below the mean. We can see how the results depend on the upper bound by comparing the code above to the code below. Since the data are naturally right-skewed, raising the upper bound raises the mean, as well as the right-skew. Thus, a greater fraction of households will fall below the mean as the upper bound is raised. 


```python
log_sample_extend = InterpolateSample(income_df, log_upper=8)
sample_extend = np.power(10, log_sample_extend)
print('Mean:', Mean(sample_extend))
print('Skew:' , Skewness(sample_extend))
print('Fraction of households below mean:' ,cdf.Prob(Mean(sample_extend)))
```

    Mean: 369110.94479665475
    Skew: 15.995937650591767
    Fraction of households below mean: 0.9807280863643045


