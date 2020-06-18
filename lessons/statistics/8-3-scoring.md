[Think Stats Chapter 8 Exercise 3](http://greenteapress.com/thinkstats2/html/thinkstats2009.html#toc77)

```python
def SimulateGame(lam):
    """Simulates a game and returns the estimated goal-scoring rate.

    lam: actual goal scoring rate in goals per game
    """
    goals = 0
    t = 0
    while True:
        time_between_goals = random.expovariate(lam)
        t += time_between_goals
        if t > 1:
            break
        goals += 1

    # estimated goal-scoring rate is the actual number of goals scored
    L = goals
    return L
```


```python
def SimulateLam(lam, iters):
    
    means = []
    for _ in range(iters):
        lam_est = SimulateGame(lam)
        means.append(lam_est)
        
    print('MSE', MeanError(means, lam))
    print('RMSE', RMSE(means, lam))
    
    
SimulateLam(2, 1000)
SimulateLam(2, 10000)
SimulateLam(2, 100000)

```

    MSE -0.061
    RMSE 1.4244297104455523
    MSE -0.011
    RMSE 1.4012137595670404
    MSE -0.00337
    RMSE 1.4134390683718914


I believe this method is unbiased, as the mean error continues to approach 0 with increased iterations.