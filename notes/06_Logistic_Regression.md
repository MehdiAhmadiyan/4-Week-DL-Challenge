# 📈 Logistic Regression

## 1. The Goal of Logistic Regression
*   Logistic regression is a learning algorithm specifically used for **binary classification** problems (where the output labels $y$ are either 0 or 1).
*   The goal is to take an input feature vector $x$ (e.g., an image) and generate a prediction $\hat{y}$.
*   $\hat{y}$ represents the estimated probability that the true label $y$ is equal to 1, given the input features $x$ (mathematically: $\hat{y}$ = P(y=1 | x)).
*   Because $\hat{y}$ acts as a probability, its value must strictly fall between 0 and 1 ($0 \le \hat{y} \le 1$).

## 2. The Parameters and the Linear Step
*   The input features are represented as an $n_x$-dimensional vector: $x \in \mathbb{R}^{n_x}$.
*   The algorithm uses two distinct parameters:
    *   $w \in \mathbb{R}^{n_x}$: A weight vector of the exact same dimension as $x$.
    *   $b \in \mathbb{R}$: A bias term, which is simply a single real number.
*   The first mathematical step is computing a linear function: $z = w^T x + b$.
*   However, using $z$ directly as the final output (like in standard linear regression) is problematic for classification. The value of $z$ can be much larger than 1 or even a large negative number, which completely violates the fundamental rules of probability.

## 3. The Sigmoid Function
*   To ensure the final output $\hat{y}$ stays strictly bounded between 0 and 1, logistic regression applies the **Sigmoid function** ($\sigma$) to the linear output $z$.
*   **Formula:**
$$\hat{y} = \sigma(z) = \frac{1}{1 + e^{-z}}$$
*   **Properties of the Sigmoid Curve:**
    *   If $z$ is a very large positive number, $e^{-z}$ approaches 0, resulting in $\sigma(z) \approx \frac{1}{1 + 0} = 1$.
    *   If $z$ is a very large negative number, $e^{-z}$ becomes a massive number, resulting in $\sigma(z) \approx 0$.
    *   When $z = 0$, the function crosses the vertical axis exactly at 0.5 ($\sigma(0) = 0.5$).

## 4. Notation Convention (A Note on Parameters)
*   In deep learning, it is highly recommended to keep $w$ and $b$ as **separate parameters**.
*   In some older machine learning courses or statistics classes, you might see an alternative convention where an extra dummy feature $x_0 = 1$ is added to the input, making $x \in \mathbb{R}^{n_x + 1}$. The parameters are then merged into a single large vector $\theta = [\theta_0, \theta_1, \dots, \theta_{n_x}]^T$, where $\theta_0$ acts as the bias $b$, and the rest act as the weights $w$.
*   While mathematically identical, keeping $w$ and $b$ separate makes implementing advanced neural networks much easier in code. Therefore, the $\theta$ convention is intentionally avoided in this course.
