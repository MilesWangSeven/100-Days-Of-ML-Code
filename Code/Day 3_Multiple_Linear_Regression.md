# 多元线性回归

此例用到的[数据](../datasets/50_Startups.csv),[代码](../Code/Day%203_Multiple_Linear_Regression.ipynb)

<p align="center">
    <img src="../Info-graphs/Day 3.png">
</p>

## 第1步：数据预处理
### 导入库
```python
import pandas as pd
import numpy as np
```
### 导入数据集
```python
dataset = pd.read_csv('../datasets/50_Startups.csv')
X = dataset.iloc[ : , :-1].values
y = dataset.iloc[ : ,  -1].values
dataset.head(5)
```
### 查看数据类型种类个数
```python
dataset['State'].unique()
```
### 将类别数据数字化
[v0.17 sklearn.preprocessing.LabelEncoder](http://lijiancheng0614.github.io/scikit-learn/modules/generated/sklearn.preprocessing.LabelEncoder.html)

[v0.20.1 sklearn.preprocessing.LabelEncoder](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.LabelEncoder.html)

[v0.17 sklearn.preprocessing.OneHotEncoder](http://lijiancheng0614.github.io/scikit-learn/modules/generated/sklearn.preprocessing.OneHotEncoder.html)

[v0.20.1 sklearn.preprocessing.OneHotEncoder](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html)
```python
from sklearn.preprocessing import LabelEncoder, OneHotEncoder
labelencoder = LabelEncoder()
X[: , 3] = labelencoder.fit_transform(X[ : , 3])
onehotencoder = OneHotEncoder(categorical_features = [3])
X = onehotencoder.fit_transform(X).toarray()
print(X.shape)
X[:5]
```
### 躲避虚拟变量陷阱
```python
X = X[ : , 1:]
```
### 拆分数据集为训练集和测试集
[v0.20.1 sklearn.model_selection.train_test_split](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.train_test_split.html)
```python
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.2, random_state = 0)
```
## 第2步：在训练集上训练多元线性回归模型
[v0.20.1 sklearn.linear_model.LinearRegression](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html)
```python
from sklearn.linear_model import LinearRegression
regressor = LinearRegression()
regressor.fit(X_train, y_train)
```
## 第3步:在测试集上预测结果
```python
y_pred = regressor.predict(X_test)
```
## 第4步：检测预测模型的准确性
```python
from sklearn.metrics import r2_score
print(r2_score(y_test,y_pred))
```
