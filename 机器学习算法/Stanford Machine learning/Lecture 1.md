## *Gradient Descent*
***Cost function***:
- $J(w, b)$: Linear regression or any functions.
***Aims***:
- $\min\limits_{w,b}J(w,b)$
***Outline***:
- Start with some$w,b$ ($w = 0, b = 0$).
- Keep changing $w,b$ to reduce $J(w,b)$.
- Until we settle at or near a minimum.

***Gradient Descent Algorithm***
$$tmp\_w = w - \alpha\frac{\partial f}{\partial w}J(w,b)$$
$$w = tmp\_w$$
$$tmp\_b = b - \alpha\frac{\partial f}{\partial b}J(w,b)$$
$$b = tmp\_b$$
*Tip*: $\alpha$ is Learning rate, range$(0, 1)$, used to control how big of step you take downhill.
*Importance*: Simultaneously update w and b. ^8e4061

***Learning Rate***
- If $\alpha$ is too small, Gradient descent may be slow.
- If $\alpha$ is too large, Gradient descent may Overshoot, never reach minimum.
*Near a local minimum*:
- Derivative becomes smaller
- Update steps become smaller
$\to$ Can reach minimum without decreasing learning rate.

***Linear Regression Model*** ^62283a
$$
\begin{align*}
f_{w,b} &= wx +b\\
J(w,b) &= \frac{1}{2m}\sum\limits_{i=1}^{m}(f_{w,b}(x^i)-y^i)^2\\
\frac{\partial f}{\partial w}J(w,b) &= \frac{1}{m}\sum\limits_{i=1}^{m}(f_{w,b}(x^i)-y^i)x^i\\
\frac{\partial f}{\partial b}J(w,b) &= \frac{1}{m}\sum\limits_{i=1}^{m}(f_{w,b}(x^i)-y^i)
\end{align*}
$$

^447bbe

***Code Achievement***
[在 Vs code 中打开](vscode://file/Users/tourbillion/Stanford_ML/Gradient_descent/Gradient_Descent.ipynb)
