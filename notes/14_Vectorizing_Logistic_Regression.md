# ⚡ Vectorizing Logistic Regression

## 1. Vectorizing Forward Propagation
To compute the predictions for all $m$ training examples simultaneously without an explicit `for` loop:
*   **Input Matrix ($X$):** Stack the training examples in columns to form an $n_x \times m$ matrix $X$.
*   **Compute $Z$:** Calculate $z^{(1)}, z^{(2)}, \dots, z^{(m)}$ simultaneously using a $1 \times m$ row vector $Z$.
    *   Math Formula: $Z = w^T X + b$
    *   Python Code: `Z = np.dot(w.T, X) + b`
    *   *Broadcasting Note:* In Python, adding the real number $b$ to a $1 \times m$ vector automatically expands (broadcasts) $b$ across all elements.
*   **Compute $A$:** Apply the sigmoid function to the matrix $Z$ to get the $1 \times m$ matrix of activations $A$.
    *   Python Code: `A = sigmoid(Z)`

## 2. Vectorizing Backward Propagation (Gradients)
Just as we vectorized the forward pass, we can compute the gradients for all $m$ examples simultaneously:
*   **Compute $dZ$:** The $1 \times m$ vector $dZ = [dz^{(1)}, dz^{(2)}, \dots, dz^{(m)}]$ is computed by simply subtracting $Y$ from $A$.
    *   Python Code: `dZ = A - Y`
*   **Compute $db$:** Take the average of all elements in the $dZ$ vector.
    *   Python Code: `db = (1/m) * np.sum(dZ)`
*   **Compute $dw$:** To get the $n_x \times 1$ vector $dw$, multiply $X$ by the transpose of $dZ$ and divide by $m$.
    *   Python Code: `dw = (1/m) * np.dot(X, dZ.T)`

## 3. Highly Efficient Implementation
By putting it all together, you can perform a single iteration of gradient descent on the entire training set without any `for` loops over the features or the training examples:

```python
# One step of gradient descent for all m examples
Z = np.dot(w.T, X) + b
A = sigmoid(Z)
dZ = A - Y
dw = (1/m) * np.dot(X, dZ.T)
db = (1/m) * np.sum(dZ)

# Parameter updates
w = w - alpha * dw
b = b - alpha * db
```

**Note:** While you successfully eliminated the loops over features and examples, you will still need one explicit, outermost `for` loop to iterate through the total number of gradient descent steps (e.g., `for iter in range(1000):`).
