[Think Stats Chapter 9 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2010.html#toc90) (resampling)

*Solution - pulled from the thinkstats solution notebook after quite a bit of trial and error!*


```python
# Solution

class DiffMeansResample(DiffMeansPermute):
    """Tests a difference in means using resampling."""
    
    def RunModel(self):
        """Run the model of the null hypothesis.

        returns: simulated data
        """
        group1 = np.random.choice(self.pool, self.n, replace=True)
        group2 = np.random.choice(self.pool, self.m, replace=True)
        return group1, group2
  
```


```python
# Solution

def RunResampleTest(firsts, others):
    """Tests differences in means by resampling.

    firsts: DataFrame
    others: DataFrame
    """
    data = firsts.prglngth.values, others.prglngth.values
    ht = DiffMeansResample(data)
    p_value = ht.PValue(iters=10000)
    print('\ndiff means resample preglength')
    print('p-value =', p_value)
    print('actual =', ht.actual)
    print('ts max =', ht.MaxTestStat())

    data = (firsts.totalwgt_lb.dropna().values,
            others.totalwgt_lb.dropna().values)
    ht = DiffMeansPermute(data)
    p_value = ht.PValue(iters=10000)
    print('\ndiff means resample birthweight')
    print('p-value =', p_value)
    print('actual =', ht.actual)
    print('ts max =', ht.MaxTestStat())
```


```python
# Solution

RunResampleTest(firsts, others)
```

    
    diff means resample preglength
    p-value = 0.1674
    actual = 0.07803726677754952
    ts max = 0.21393028325881147
    
    diff means resample birthweight
    p-value = 0.0003
    actual = 0.12476118453549034
    ts max = 0.1335955672457132



```python
.187, 0
```

The resampling model does not substantially affect the results. Comparing resampling to the old method, the p-value for differences in pregnancy length moves from .187 to .167; for birth weight, it stays < .001. 

*Original attempt*


```python
# class DiffMeansPermute(thinkstats2.HypothesisTest):

#     def TestStatistic(self, data):
#         group1, group2 = data
#         test_stat = abs(group1.mean() - group2.mean())
#         return test_stat

#     def MakeModel(self):
#         group1, group2 = self.data
#         self.n, self.m = len(group1), len(group2)
#         self.pool = np.hstack((group1, group2))
    
#     #Need to override this
#     def RunModel(self):
#         np.random.shuffle(self.pool)
#         data = self.pool[:self.n], self.pool[self.n:]
#         return data
```


```python
# class DiffMeansResample(DiffMeansPermute):
    
#     def RunModel(self):
#         #np.random.shuffle(self.pool)
#         #data = self.pool[:self.n], self.pool[self.n:]
        
#         #Taking from FalseNegRate
#         sample1 = thinkstats2.Resample(group1)
#         sample2 = thinkstats2.Resample(group2)
#         return sample1, sample2
```
