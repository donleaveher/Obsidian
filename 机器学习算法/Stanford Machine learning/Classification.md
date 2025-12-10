--## Logistics regression

### Example
- 1 and 0 represent tumor malignant or not.

***Sigmoid Function(Logistic function)***
- Outputs between 0 and 1
$$g(z)=\frac{1}{1+e^{-z}}\quad 0<g(z)<1 $$
![[Multiple features(variables)#^fcae3f]]
$$\begin{align*}
z &=\vec w\cdot\vec x+b\\
g(\vec w\cdot\vec x+b)&=\frac{1}{1+e^{-(\vec w\cdot\vec x+b)}}
\end{align*}
$$
### Decision boundary
- Setting a threshold to determine $\bar y$ is 1 or 0.

***Logistic Loss Function***
$$L(f_{\vec w,b}(\vec x^{(i)}),y^{(i)})=\begin{cases}-\log(f_{\vec w,b}(\vec x^{(i)}))&\text{if\;}y^{(i)} = 1\\-\log(1-f_{\vec w,b}(\vec x^{(i)}))&\text{if\;}y^{(i)} = 0\end{cases}$$
Case 1 $y = 1$: ^abb7a3
- As $f_{\vec w,b}(\vec x^{(i)})\to 1$ then ${loss}\to 0$
- As $f_{\vec w,b}(\vec x^{(i)})\to 0$ then ${loss}\to\infty$
Case 2 $y=0$:
- As $f_{\vec w,b}(\vec x^{(i)})\to 1$ then ${loss}\to\infty$
- As $f_{\vec w,b}(\vec x^{(i)})\to 0$ then ${loss}\to 0$

***Cost Function***
$$J(\vec w,b)=\frac{1}{m}\sum_{i = 1}^{m}L(f_{\vec w,b}(\vec x^{(i)}),y^{(i)})$$
***Simplified Cost Function***
$$\begin{align*}
L(f_{\vec w,b}(\vec x^{(i)}),y^{(i)}) &= -y^{(i)}\log(f_{\vec w,b}(\vec x^{(i)}))-(1-y^{(i)})\log(1-f_{\vec w,b}(\vec x^{(i)}))\\
J(\vec w,b)&=\frac{1}{m}\sum_{i = 1}^{m}[L(f_{\vec w,b}(\vec x^{(i)}),y^{(i)})]
\end{align*}
$$

^9bdce0

***Similar to Linear Cost Function Gradient Descent***
![[Lecture 1#^447bbe]] ^cdd0a7

### Reduce Overfitting
- Collect more training examples.
- Select features to include/exclude.
- Regularization: Keep all features and reduce some of their impact
### Regularization Linear Regression Function
$$
\begin{align*}
\min\limits_{\vec w,b}J(\vec w, b) &= \min\limits_{\vec w, b}\frac{1}{2m}\sum\limits_{i=1}^{m}(f_{\vec w,b}(x^{(i)})-y^{(i)})^2+\frac{\lambda}{2m}\sum_{j=1}^{n}w_j^2\\
\frac{\partial(J(\vec w,b))}{\partial(w_j)} &=\frac{1}{m}\sum\limits_{i=1}^{m}(f_{\vec w,b}(x^{(i)}-y^{(i)})x^{(i)} + \frac{\lambda}{m}w_j\\
\frac{\partial(J(\vec w,b))}{\partial(b)} &=\frac{1}{m}\sum\limits_{i=1}^{m}(f_{\vec w,b}(x^{(i)})-y^{(i)})
\end{align*}
$$

^aab0f9

![[Lecture 1#^8e4061]]
### Implementing Gradient Descent
$$w_j = w_j(1-\alpha\frac{\lambda}{m})- \frac{\alpha}{m}\sum\limits_{i=1}^{m}(f_{\vec w,b}(x^{(i)}-y^{(i)})x^{(i)}$$
