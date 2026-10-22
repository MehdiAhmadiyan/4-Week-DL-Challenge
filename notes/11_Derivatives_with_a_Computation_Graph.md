# 📈 Computing Derivatives with a Computation Graph

## 1. The Core Concept: Backpropagation
*   In the previous step, we computed the output of the function $J(a, b, c) = 3(a + bc)$ through a **forward pass** (left-to-right). The intermediate variables were $u = bc$ and $v = a + u$.
*   To find the derivatives of the final output $J$ with respect to the initial inputs ($a, b, c$), we perform a **backward pass** (right-to-left).
*   In deep learning terminology, computing these derivatives by moving backward through the graph is called **Backpropagation**.

## 2. Step-by-Step Derivative Calculation (Right-to-Left)

### Step 1: Derivative of $J$ with respect to $v$
*   Function: $J = 3v$.
*   If we bump up $v$ by $0.001$, $J$ goes up by $3 \times 0.001 = 0.003$.
*   Therefore, the slope is 3: $\frac{dJ}{dv} = 3$.

### Step 2: Derivative of $J$ with respect to $a$
*   Function: $v = a + u$.
*   How does changing $a$ affect $J$? We use the **Chain Rule** from calculus.
*   The chain rule states that the total change in $J$ is the product of how much $a$ affects $v$, multiplied by how much $v$ affects $J$:
    $$\frac{dJ}{da} = \frac{dJ}{dv} \times \frac{dv}{da}$$
*   Since $v = a + u$, if we increase $a$ by $1$, $v$ increases by $1$. So, $\frac{dv}{da} = 1$.
*   Applying the chain rule: $\frac{dJ}{da} = 3 \times 1 = 3$.

### Step 3: Derivative of $J$ with respect to $u$
*   Using the exact same chain rule logic:
    $$\frac{dJ}{du} = \frac{dJ}{dv} \times \frac{dv}{du}$$
*   Since $v = a + u$, the derivative $\frac{dv}{du} = 1$.
*   Therefore: $\frac{dJ}{du} = 3 \times 1 = 3$.

### Step 4: Derivative of $J$ with respect to $b$ and $c$
*   Function: $u = bc$.
*   To find how $b$ affects $J$, we apply the chain rule again, using the previously computed $\frac{dJ}{du}$:
    $$\frac{dJ}{db} = \frac{dJ}{du} \times \frac{du}{db}$$
*   Since $u = bc$, the derivative of $u$ with respect to $b$ is simply $c$. Given $c = 2$, $\frac{du}{db} = 2$.
*   Applying the chain rule: $\frac{dJ}{db} = 3 \times 2 = 6$.
*   Similarly for $c$: $\frac{dJ}{dc} = \frac{dJ}{du} \times \frac{du}{dc} = 3 \times 3 = 9$.

## 3. Python Coding Convention (Crucial)
*   When writing Python code for backpropagation, you will constantly compute derivatives of the final output variable (like $J$) with respect to various intermediate variables (like $v, a, u, b$).
*   Instead of writing mathematically accurate but excessively long variable names in your code (like `dFinalOutputVar_dvar`), deep learning practitioners use a highly simplified naming convention:
    *   $\frac{dJ}{dv}$ is simply coded as **`dv`**.
    *   $\frac{dJ}{da}$ is simply coded as **`da`**.
    *   $\frac{dJ}{db}$ is simply coded as **`db`**.
*   **Rule of Thumb:** In your Python code, any variable named `dSomething` always represents the derivative of the *final cost function* with respect to *that something*.
