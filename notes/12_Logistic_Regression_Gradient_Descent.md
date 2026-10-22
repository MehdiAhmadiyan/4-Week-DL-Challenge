# 📉 Logistic Regression: Gradient Descent Implementation

## 1. Gradient Descent on a Single Example
To implement gradient descent for logistic regression, we first need to understand how to compute the derivatives (gradients) for a single training example ($x, y$). 

### The Forward Pass
First, we compute the loss using the computation graph:
1.  Compute the linear combination: $z = w^T x + b$. (Assuming two features, this is $z = w_1x_1 + w_2x_2 + b$).
2.  Apply the activation function: $a = \sigma(z)$ *(Note: $a$ is the exact same thing as $\hat{y}$)*.
3.  Compute the loss: $L(a, y) = -(y \log(a) + (1 - y) \log(1 - a))$.

### The Backward Pass (Computing Derivatives)
Using the chain rule, we compute the derivatives backwards:
1.  **Derivative of Loss wrt $a$:** 
    `da` = $\frac{dL}{da} = -\frac{y}{a} + \frac{1 - y}{1 - a}$.
2.  **Derivative of Loss wrt $z$:** 
    By applying the chain rule (`dz` = $\frac{dL}{da} \times \frac{da}{dz}$), the math simplifies beautifully to:
    `dz` = $\frac{dL}{dz} = a - y$. *(This is the most crucial formula to remember)*.
3.  **Derivative of Loss wrt Parameters ($w, b$):**
    Using the chain rule again with `dz`:
    *   `dw1` = $\frac{\partial L}{\partial w_1} = x_1 \times dz$.
    *   `dw2` = $\frac{\partial L}{\partial w_2} = x_2 \times dz$.
    *   `db` = $\frac{\partial L}{\partial b} = dz$.

### The Parameter Update
Once the derivatives are computed, update the parameters using the learning rate ($\alpha$):
*   $w_1 := w_1 - \alpha \times dw_1$.
*   $w_2 := w_2 - \alpha \times dw_2$.
*   $b := b - \alpha \times db$.

## 2. Gradient Descent on $m$ Examples
In practice, we do not train on just one example; we train on an entire dataset of $m$ examples. The derivative of the overall cost function $J$ is simply the **average** of the derivatives computed for each individual training example.

### The Code Structure (Using explicit `for` loops)
To implement this in code, you would use accumulators to sum up the derivatives across all examples, and then divide by $m$:

```python
J = 0; dw1 = 0; dw2 = 0; db = 0

for i = 1 to m:
    # Forward pass for the i-th example
    z[i] = w^T x[i] + b
    a[i] = sigmoid(z[i])
    
    # Accumulate cost
    J += -[ y[i] * log(a[i]) + (1 - y[i]) * log(1 - a[i]) ]
    
    # Backward pass for the i-th example
    dz[i] = a[i] - y[i]
    
    # Accumulate derivatives
    dw1 += x1[i] * dz[i]
    dw2 += x2[i] * dz[i]
    db += dz[i]

# Compute averages
J /= m
dw1 /= m
dw2 /= m
db /= m

# Update parameters
w1 = w1 - alpha * dw1
w2 = w2 - alpha * dw2
b = b - alpha * db
```

## 3. The Need for Vectorization
*   **The Problem:** The implementation above requires two explicit `for` loops: 
    1.  A loop over the $m$ training examples.
    2.  A loop over the $n$ features (to compute $dw_1, dw_2, \dots, dw_n$).
*   **The Bottleneck:** Writing explicit `for` loops in Python is highly inefficient and slow, especially when dealing with massive deep learning datasets.
*   **The Solution:** To make the algorithm run efficiently, deep learning relies heavily on **Vectorization** techniques to eliminate these explicit `for` loops entirely.
