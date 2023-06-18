---
layout: post
title: 'Project: A/B Test'
type: project
---

# Introduction

In this small project, we will take a look at how to perform an A/B test. To do so, we will use [synthetic data](https://www.kaggle.com/datasets/sergylog/ab-test-data) borrowed on Kaggle.

```python
import random
import numpy as np
import pandas as pd
from scipy.stats import ttest_ind, ttest_rel, shapiro, mannwhitneyu, wilcoxon

random.seed(42)
np.random.seed(42)
```


```python
data = pd.read_csv("/kaggle/input/ab-test-data/AB_Test_Results.csv")
```

# Hypotheses
Null: 'control' and 'variant' groups have no significant difference in revenue.

Alternative: 'control' and 'variant' groups have a significant difference in revenue.

# Assumptions to check

1. Do we have missing data? (no)
2. Is data balanced? (yes, we have roughly equal number of 'control' and 'variant' data points)
3. Are data rows independent? (no, we have multiple measurements with the same user id)
4. Are some users in both groups? (yes)
5. Does revenue have a normal distribution? (no)


```python
# no missing data
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



```python
# roughly equal data points in both groups
data.value_counts(['VARIANT_NAME'])
```




    VARIANT_NAME
    variant         5016
    control         4984
    dtype: int64




```python
# some users have multiple measurements
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




```python
# user 3 is both in control and variant group
data.groupby(['USER_ID', 'VARIANT_NAME']).sum().head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>REVENUE</th>
    </tr>
    <tr>
      <th>USER_ID</th>
      <th>VARIANT_NAME</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <th>control</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">3</th>
      <th>control</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>variant</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <th>variant</th>
      <td>0.0</td>
    </tr>
    <tr>
      <th>5</th>
      <th>variant</th>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# normality test
# scipy produces a warning for sample size > 5000
# solution: randomly sample 5000
shapiro(data[['REVENUE']].sample(5000))
```




    ShapiroResult(statistic=0.01863241195678711, pvalue=0.0)



# Hypothesis testing

Since we have users that fell both into control and variant groups, we will use the difference between the average revenues of the same users in control and variant groups respectively.

Also, the revenue variable does not follow a normal distribution, so we will use a Wilcoxon's nonparametric test


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



We have a rather high p-value of 0.81, which basically means the difference in revenue between groups is not significant at all. But let us try to compare the two groups as independent samples using Wilcoxon test's two-sample version: mannwhitneyu


```python
mannwhitneyu(control, variant)
```




    MannwhitneyuResult(statistic=array([7750479.]), pvalue=array([0.4469186]))



Again, we do not observe a significant difference between the two groups.

# Conclusion
We have checked important assumptions to determine what statistical significance tests are appropriate. We tried two different tests, one where we paired the samples by user ids and another where we pretended to have independent samples. None of the tests showed a significant difference in revenue between the control and variant group.