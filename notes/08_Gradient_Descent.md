# 📉 Gradient Descent

## 1. The Goal of Gradient Descent
*   The overall cost function for logistic regression is $J(w, b)$.
*   The primary objective of the learning process is to find the specific values for the parameters $w$ and $b$ that minimize the cost function $J(w, b)$ (making it as small as possible).
*   **Convexity:** The cost function $J(w, b)$ for logistic regression is a **convex function**. This means it is shaped like a single big bowl and has only one global optimum, completely avoiding the problem of multiple local optima. This convexity is the main reason this specific cost function is used.

## 2. How the Algorithm Works
Gradient descent starts with an initial guess for the parameters and iteratively updates them to find the minimum.

1.  **Initialization:** For logistic regression, it is standard practice to initialize the parameters $w$ and $b$ to $0$. Because the function is convex, any initialization (even random) will eventually lead to the same global optimum.
2.  **Taking Steps:** From the initial point, the algorithm calculates the slope (derivative) of the cost function.
3.  It then takes a step in the direction of the **steepest descent** (downhill) to reach a new point.
4.  This process is repeated (iterated) until the algorithm converges to the global minimum (the bottom of the bowl).

## 3. The Mathematical Update Rule
The core of the gradient descent algorithm is repeating the following update rule until convergence:

$$w := w - \alpha \frac{\partial J(w, b)}{\partial w}$$
$$b := b - \alpha \frac{\partial J(w, b)}{\partial b}$$

*   **The Assignment Operator ($:=$):** Means we are updating the value of the variable on the left with the newly calculated value on the right.
*   **Learning Rate ($\alpha$):** This parameter controls how big of a step the algorithm takes downhill on each iteration.
*   **Derivative ($\frac{\partial J}{\partial w}$):** This term represents the slope of the function at the current parameter values, telling the algorithm which direction is downhill.

### Intuition Behind the Update:
*   If the current slope ($\frac{\partial J}{\partial w}$) is **positive**, subtracting it makes $w$ smaller, moving it leftwards down the curve.
*   If the current slope ($\frac{\partial J}{\partial w}$) is **negative**, subtracting a negative number adds to $w$, moving it rightwards down the curve.
*   In both cases, it moves towards the minimum.

## 4. Calculus Notation vs. Code Variables
*   **Derivatives vs. Partial Derivatives:** In calculus, if a function has only one variable (like $J(w)$), its slope is written with a standard lowercase $d$ as $\frac{dJ}{dw}$. If a function has multiple variables (like $J(w, b)$), the slope with respect to one variable is mathematically written using the partial derivative symbol ($\partial$) as $\frac{\partial J}{\partial w}$. Practically, they mean the exact same thing: the slope of the function.
*   **Code Implementation:** When writing Python code, we do not use mathematical symbols. Instead, we use a standard naming convention:
    *   The quantity $\frac{\partial J(w, b)}{\partial w}$ is simply coded as the variable `dw`.
    *   The quantity $\frac{\partial J(w, b)}{\partial b}$ is simply coded as the variable `db`.
*   Therefore, the code update looks like:
    ```python
    w = w - alpha * dw
    b = b - alpha * db
    ```
