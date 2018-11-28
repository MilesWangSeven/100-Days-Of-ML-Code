# 数据预处理

此例用到的[数据](../datasets/Data.csv),[代码](../Code/Day%201_Data_Preprocessing.ipynb)

<p align="center">
    <img src="../Info-graphs/Day 1.jpg">
</p>

如图所示，通过6步完成数据预处理。

## 第1步:导入库
```python
import numpy as np
import pandas as pd
```
## 第2步：导入数据集
```python
dataset = pd.read_csv('../datasets/Data.csv')
X = dataset.iloc[ : , : -1].values
y = dataset.iloc[ : , -1].values
print('X.shape = {}'.format(X.shape))
print(X)
print(y)
```
## 第3步：处理丢失数据
[v0.17 sklearn.preprocessing.Imputer](http://lijiancheng0614.github.io/scikit-learn/modules/generated/sklearn.preprocessing.Imputer.html)

[v0.20.1 sklearn.impute.SimpleImputer](https://scikit-learn.org/stable/modules/generated/sklearn.impute.SimpleImputer.html)

```python
from sklearn.preprocessing import Imputer
imputer = Imputer(missing_values = 'NaN', strategy = 'mean', axis = 0)
imputer = imputer.fit(X[ : , 1:3])
X[ : , 1:3] = imputer.transform(X[ : , 1:3])
print(X)
```
## 第4步：解析分类数据
[v0.17 sklearn.preprocessing.LabelEncoder](http://lijiancheng0614.github.io/scikit-learn/modules/generated/sklearn.preprocessing.LabelEncoder.html)

[v0.20.1 sklearn.preprocessing.LabelEncoder](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.LabelEncoder.html)

[v0.17 sklearn.preprocessing.OneHotEncoder](http://lijiancheng0614.github.io/scikit-learn/modules/generated/sklearn.preprocessing.OneHotEncoder.html)

[v0.20.1 sklearn.preprocessing.OneHotEncoder](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html)

```python
from sklearn.preprocessing import LabelEncoder, OneHotEncoder
labelencoder_X = LabelEncoder()
X[ : , 0] = labelencoder_X.fit_transform(X[ : , 0])
print(X[ : , 0])
```
### 创建虚拟变量
```python
onehotencoder = OneHotEncoder(categorical_features = [0])
X = onehotencoder.fit_transform(X).toarray()
labelencoder_y = LabelEncoder()
y = labelencoder_y.fit_transform(y)
print(X)
print('X.shape = {}'.format(X.shape))
print(y)
```
## 第5步：拆分数据集为训练集合和测试集合
[v0.20.1 sklearn.model_selection.train_test_split¶](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.train_test_split.html)

```python
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.2, random_state = 0)
print('X_train.shape = {}'.format(X_train.shape))
print('X_test.shape = {}'.format(X_test.shape))
print('y_train.shape = {}'.format(y_train.shape))
print('y_test.shape = {}'.format(y_test.shape))
```
## 第6步：特征量化
[v0.20.1 sklearn.preprocessing.StandardScaler](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.StandardScaler.html)

```python
from sklearn.preprocessing import StandardScaler
sc_X = StandardScaler()
X_train = sc_X.fit_transform(X)
X_test = sc_X.transform(X_test)
print(X_train)
print(X_test)
```
