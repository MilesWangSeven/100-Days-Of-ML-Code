# 简单线性回归

<p align="center">
    <img src="../Info-graphs/Day 2.jpg">
</p>

## 第一步：数据预处理
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

dataset = pd.read_csv('../datasets/studentscores.csv')
X = dataset.iloc[ : , :-1].values
y = dataset.iloc[ : , -1].values

from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y,test_size = 1/4, random_state=0)
dataset.head(5)
```
## 第二步：训练集使用简单线性回归模型来训练
[v0.20.1 sklearn.linear_model.LinearRegression](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html)
```python
from sklearn.linear_model import LinearRegression
regessor = LinearRegression()
regessor.fit(X_train, y_train)
```
## 第三步:预测结果
```python
y_pred = regessor.predict(X_test)
```
## 第四步:可视化
### 测试结果可视化
```python
%matplotlib inline
plt.scatter(X_train, y_train, color = 'red')
plt.plot(X_train, regessor.predict(X_train), color='blue')
plt.show()
```
### 测试结果可视化
```python
plt.scatter(X_test, y_test, color = 'red')
plt.plot(X_test, y_pred, color = 'blue')
plt.show()
```
