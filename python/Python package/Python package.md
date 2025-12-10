***Pandas***
```python
import pandas as pd
cvs_path = 'path.csv'
df = pd.read_cvs(cvs_path)
df.head()
{key1:[], key2:[], key3:[],......}
df[['Artist','Length', 'Genre']]
df.iloc[i][j]
df.loc[row,'key']
df.iloc[1:2][3:4] # can use slice
df.loc[0:2, 'key1':'key2'] two sides inclusive
df = df[df['key']>1979] # conditional
df.to_csv

DataFrame.dropna(axis=0, how='any', thresh=None, subset=None, inplace=False)
```


***Numpy***
```python
import numpy as np

x = np.arrange(0,20,1)
# Generate a array from 0 to 19, step = 1
y = 1 + x**2
# Each elements in x are mutiple itself and plus 1 
X = x.reshape(-1, 1)
# [0, 1, 2] to [[0],[1],[2]]
X = np.c_[x, x**2, x**3]
# concat each array in column
np.ptp(X, axis = 0)

np.exp(array/value)
def sigmoid(z):
	# z is array
	g = 1/(1+np.exp(-z))
	return g
np.linspace(-2,2,num = 9)
np.linespace(0,2*np.pi,100)
```

***Matplotlib***
```python
import Matplotlib as plt

plt.scatter(x, y, marker='x', c='r', label = "Actual Value")
# marker can be changed to dot or etc.
# c represent color.
plt.plot(x,X@model_w + model_b, c = ' ', label = " ")
plt.title(" ")
plt.xlabel(" ")
plt.ylabel(" ")

fig, ax = plt.subplot(m, n, figsize=(12,3), sharey = True)
# fig represent the whole graph, ax is an array, stores  m * n subgraphs
# sharey means all the graphs use the same Y axis   
for i in range(len(ax)):
	ax[i].scatter(X[:,i],y)
	ax[i].set_xlabel(X_features[i])
```

***Scikit-Learn***
```python
from sklearn.linear_model import SGDRegressor
from sklearn.preprocessing import StandardScaler
# create a StandardScaler object
scaler = StandardScaler()
X_norm = scaler.fit_transform(X_train)
# fit(): StandardScaler 首先会计算 X_train 中每一列（每个特征）的平均值和标准差。
# transform(): 然后，它会用上一步计算出的平均值和标准差来对 X_train 的每一列数据进行转换。转# 换公式为：z=(x−μ)/σ，其中 μ 是均值，σ 是标准差。

# create and fit the regression model
sgdr = SGDRegressor(max_iter = 1000)
# create a SGDRegressor object and the iteration times = 1000
# SGDR (Stochastic Gradient Descent Regression)
sgdr.fit(X_norm, y_train)

sgdr.intercept_ : intercept, b
sgdr.coef_ : coefficients, w

sgdr.predict(X_norm): using predict method to predict the train_data
y_pred = np.dot(X_norm, w_norm) + b_norm

(y_pred == y_pred_sgd).all()
# y_pred == y_pred_sgd -> [True, True, True, ...]
# .all() : every single element in the array is True, return true, else false
```

***Compute Cost Logistic***
```python
def comput_cost_logistic(X, y, w, b):
	# X.shape = (m,n)
	m = X.shape[0]
	cost = 0.0
	for i in range(m):
		z = np.dot(X[i],w)+b
		f_z = sigmoid(z)
		cost = cost - y[i]*np.log(f_z) - (1 - y[i])*np.log(1-f_z)
	cost = cost/m
	return cost
```
![[Classification#^9bdce0]]

![[Lecture 1#^447bbe]]

***Compute Gradient Logistic***
```python
def compute_gradient_logistic(X,y,w,b):
	m,n = X.shape
	dj_dw = np.zeros((n,))
	dj_db = 0.0
	for i in range(m):
		f_wb_i = sigmoid(np.dot(X[i],w)+b)
		err_i = f_wb_i - y[i] 
		for j in range(n):
			dj_dw[j] = dj_dw[j] + err_i*X[i,j]
		dj_db = dj_db+err_i
	dj_dw = dj_dw/m
	dj_db = dj_db/m
	return dj_dw, dj_db
```