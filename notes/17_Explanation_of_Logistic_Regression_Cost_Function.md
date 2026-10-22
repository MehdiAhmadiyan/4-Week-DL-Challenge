# 🧠 Explanation of Logistic Regression Cost Function (Optional)

## 1. Interpreting the Output as a Probability
*   In logistic regression, the prediction $\hat{y}$ is interpreted as the probability that the true label $y$ is equal to 1, given the input features $x$.
*   Mathematically: $\hat{y} = P(y=1 \mid x)$.
*   Because $y$ can only be 0 or 1 (binary classification), this gives us two distinct cases:
    *   If $y = 1$: $P(y \mid x) = \hat{y}$.
    *   If $y = 0$: $P(y \mid x) = 1 - \hat{y}$.

## 2. Compressing into a Single Equation
*   To simplify the math, we can elegantly summarize both of the above cases into a single mathematical equation:
$$P(y \mid x) = \hat{y}^y (1 - \hat{y})^{(1 - y)}$$
*   **Why this works perfectly:**
    *   If $y = 1$, the second term $( 1 - \hat{y} )^0$ becomes 1, and the formula simplifies to exactly $\hat{y}$.
    *   If $y = 0$, the first term $\hat{y}^0$ becomes 1, and the formula simplifies to exactly $1 - \hat{y}$.

## 3. Deriving the Loss Function
*   The logarithm is a strictly monotonically increasing function. This means that maximizing the logarithm of a probability yields the exact same optimal parameters as maximizing the probability itself.
*   Taking the log of our single equation gives:
$$\log P(y \mid x) = y \log(\hat{y}) + (1 - y) \log(1 - \hat{y})$$
*   Notice that this equation is exactly the negative of the Loss function we defined earlier: $-L(\hat{y}, y)$.
*   In machine learning optimization, we typically want to **minimize** a loss function rather than maximize it. Therefore, we drop the negative sign, giving us the standard logistic loss function $L(\hat{y}, y)$.

## 4. Maximum Likelihood Estimation (MLE) on $m$ Examples
*   Assuming the $m$ training examples are independent and identically distributed (IID), the probability of the entire dataset is the product of the individual probabilities.
*   Taking the log turns this massive product into a sum:
$$\log P(\text{labels in training set}) = \sum_{i=1}^m \log P(y^{(i)} \mid x^{(i)}) = -\sum_{i=1}^m L(\hat{y}^{(i)}, y^{(i)})$$
*   In statistics, the principle of **Maximum Likelihood Estimation (MLE)** states that we should choose the parameters that maximize this probability.
*   Mathematically, maximizing this sum is identical to **minimizing** the overall cost function $J(w, b)$. (The extra $\frac{1}{m}$ factor is simply added for convenience to compute the average cost).
