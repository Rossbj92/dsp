[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

How many people are between 5'10" and 6'1"?


```python
#% below 5'10
min_height = dist.cdf((5*12+10)*2.54)
max_height = dist.cdf((6*12+1)*2.54)
percent_in_range = max_height - min_height
print("{}% of people are within 5'10 and 6'1".format(round(percent_in_range*100),2))
```

    34.0% of people are within 5'10 and 6'1
