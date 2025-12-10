$x_j = j^{th}$ feature
$n =$ number of feature
$\vec{x}^{(i)} =$ features of $i^{th}$ training example

***Original Model:***
$$\begin{align*}
{Previously:} f_{w,b}(x) &= wx + b\\
f_{w,b}(x) &= w_1x_2 + w_2x_2 + w_3x_3 + w_4x_4 +b\\
{General\,function}:f_{w,b}(x)&=w_1x_2 + w_2x_2+\ldots+w_nx_n+b\\
{Without\,vectoriztion}:f_{\vec w,b}&= \sum_{j=1}^nw_jx_j+b
\end{align*}
$$
***Vectorization*** ^baabc9
$$\begin{align*}
\vec{w} &= [w_1, w_2,\ldots,w_n]\\
\vec{x} &= [x_1, x_2,\ldots,w_n]\\
f_{\vec w,b}(\vec x) &= \vec w\cdot \vec x+b
\end{align*}$$

^fcae3f

```python
import numpy as np
Create array
w = np.array([1.0,2.0,3.0])
x = np.array([10, 20, 30])

Without vectorization
for i in range(0,n):
	f = j + w[i] * x[i]
f = f + b
Vectorization
f = np.dot(w, x) + b
```
![[Lecture 1#^447bbe]]
## Features scaling
***Divide by the Maximum***
$$\begin{align*}
300\le &x_1\le2000\quad &0\le &x_2\le5\\
x_{1,scaled}&=\frac{x_1}{2000}\quad &x_{2,scaled}&=\frac{x_2}{5}\\
0.15\le& x_{1,scaled}\le 1\quad &0\le &x_{2,scaled}\le1\\
\end{align*}
$$
***Mean normalization***

$$\begin{align*}
300&\le x_1\le2000\quad &0\le &x_2\le5\\
x_{1,scaled}&=\frac{x_1-\mu_1}{2000}\quad &x_{2,scaled}&=\frac{x_2-\mu_2}{5}\\
-0.18&\le x_{1,scaled}\le 0.82\quad &-0.46\le &x_{2,scaled}\le0.54\\
\end{align*}
$$
***Z-score normalization***
$$\begin{align*}
x_j^{(i)} &=\frac{x_j^{(i)}-\mu_j}{\sigma_j}\\
\mu_j &= \frac{1}{m}\sum_{i=0}^{m-1}(x_j^{(i)})\\
\sigma_j^2&= \frac{1}{m}\sum_{i=0}^{m-1}(x_j^{(i)}-\mu_j)^2
\end{align*}$$
***
## Feature engineering
***Feature engineering***: Using intuition to design new features, by transforming or combining original features. 
***Polynominal regression***
$$\begin{align*}
f_{\vec w,b}(x) &= w_1x+w_2x^2+w_3x^3+b\\
f_{\vec w,b}(x) &= w_1x+w_2\sqrt x +b
\end{align*}$$
