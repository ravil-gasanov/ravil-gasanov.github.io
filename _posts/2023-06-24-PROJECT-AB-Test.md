---
layout: post
title: 'PROJECT: A/B Test'
type: project
---

In this mini-project, I first explain the concept of A/B testing. After that I provide a concrete example to tackle the technical details.

To provide a minimal example without distracting elements, I picked a [synthetic data set](https://www.kaggle.com/datasets/sergylog/ab-test-data).

# Concept
A/B tests are a rigorous way to compare two versions of a product. 

For example, let's say we would like to know which color theme on our landing page leads to more sales, blue or purple. To determine this, we would have to compare the color themes with *all other things being equal*.

It is straightforward for the variables we directly control, e.g., the other website elements, we just keep them fixed for both versions. 

Less obvious is how we should deal with variables we can't control. For example, the user's display or the lighting in their office. We do not even have access to most of this kind of information. But the solution is elegant. We just randomize these aspects. If we choose to show a specific color theme to users on a random basis, any external effects on sales will come down to the same average for both groups, and the only difference (if there is any) will be due to the color theme.

# A/B Test Experiment
For an interactive and better formatted experience, check out the [Kaggle notebook](https://www.kaggle.com/code/ravilgasanov/1-0-rg-ab-test) version of the experiment.

## Hypotheses
Null: 'control' and 'variant' groups have no significant difference in revenue.

Alternative: 'control' and 'variant' groups have a significant difference in revenue.

## Assumptions to check

1. Do we have missing data? (no)
2. Is data balanced? (yes, we have roughly equal number of 'control' and 'variant' data points)
3. Are data rows independent? (no, we have multiple measurements with the same user id)
4. Are some users in both groups? (yes)
5. Does revenue have a normal distribution? (no)

### No missing data
```python

data.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 10000 entries, 0 to 9999
    Data columns (total 3 columns):
     #   Column        Non-Null Count  Dtype  
    ---  ------        --------------  -----  
     0   USER_ID       10000 non-null  int64  
     1   VARIANT_NAME  10000 non-null  object 
     2   REVENUE       10000 non-null  float64
    dtypes: float64(1), int64(1), object(1)
    memory usage: 234.5+ KB



### Roughly equal data points in both groups
```python
data.value_counts(['VARIANT_NAME'])
```




    VARIANT_NAME
    variant         5016
    control         4984
    dtype: int64




### Some users have multiple measurements
```python
data.value_counts(['USER_ID'])
```
    USER_ID
    9101       6
    668        6
    5652       6
    8359       6
    4879       6
              ..
    4682       1
    4684       1
    4687       1
    4689       1
    5525       1
    Length: 6324, dtype: int64



### User 3 is both in control and variant group
```python
data.groupby(['USER_ID', 'VARIANT_NAME']).sum().head()
```

    | USER_ID | VARIANT_NAME | REVENUE |
    |---------|--------------|---------|
    |    2    |   control    |   0.0   |
    |    3    |   control    |   0.0   |
    |    3    |   variant    |   0.0   |
    |    4    |   variant    |   0.0   |
    |    5    |   variant    |   0.0   |

### Normality test
```python
# scipy produces a warning for sample size > 5000
# solution: randomly sample 5000
shapiro(data[['REVENUE']].sample(5000))
```
    ShapiroResult(statistic=0.01863241195678711, pvalue=0.0)



## Hypothesis testing

Since we have users that fell both into control and variant groups, we will use the difference between the average revenues of the same users in control and variant groups respectively.

Also, the revenue variable does not follow a normal distribution, so we will use the Wilcoxon's nonparametric test.


```python
data_user_average = data.groupby(['USER_ID', 'VARIANT_NAME']).mean()
```


```python
control = data_user_average.query("VARIANT_NAME == 'control'")
variant = data_user_average.query("VARIANT_NAME == 'variant'")
```


```python
pairs = pd.merge(control, variant, on = "USER_ID", how = "inner", suffixes = ("_control", "_variant"))
```


```python
wilcoxon(pairs['REVENUE_control'] - pairs['REVENUE_variant'])
```
    WilcoxonResult(statistic=715.0, pvalue=0.812822440169386)



We have a rather high p-value of 0.81, which basically means the difference in revenue between groups is not significant at all. But let us try to compare the two groups as independent samples using Wilcoxon test's two-sample version.


```python
mannwhitneyu(control, variant)
```
    MannwhitneyuResult(statistic=array([7750479.]), pvalue=array([0.4469186]))



Again, we do not observe a significant difference between the two groups.

# Conclusion
We have checked important assumptions to determine what statistical significance tests are appropriate. We tried two different tests, one where we paired the samples by user ids and another where we pretended to have independent samples. None of the tests showed a significant difference in revenue between the control and variant group.
