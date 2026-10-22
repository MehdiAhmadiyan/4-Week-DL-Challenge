# 📉 Logistic Regression Cost Function

## 1. The Setup and Goal
*   To train the parameters $w$ and $b$ of a logistic regression model, we must define a cost function].
*   Given a training set of $m$ examples, the goal is to find parameters $w$ and $b$ so that the predictions ($\hat{y}^{(i)}$) are as close as possible to the ground truth labels ($y^{(i)}$)].
*   **Notation:** The superscript $(i)$ wrapped in parentheses—such as $x^{(i)}$, $y^{(i)}$, or $\hat{y}^{(i)}$—denotes data associated with the $i$-th training example].

## 2. The Loss Function (Single Example)
*   The **Loss function** (or error function), denoted as $L(\hat{y}, y)$, measures how well the algorithm is performing on a **single** training example].
*   **Why not Squared Error?** In linear regression, we often use the squared error: $L(\hat{y}, y) = \frac{1}{2}(\hat{y} - y)^2$]. However, if we use this for logistic regression, the optimization problem becomes **non-convex**. This means it will have multiple local optima, and the Gradient Descent algorithm may fail to find the global optimum.
*   **The Logistic Loss Function:** To ensure a convex optimization problem (which is much easier to optimize), logistic regression uses the following loss function]:
$$L(\hat{y}, y) = -(y \log(\hat{y}) + (1 - y) \log(1 - \hat{y}))$$

### Intuition Behind the Loss Function
We want this loss function to be as small as possible. Let's look at the two possible cases for the true label $y$]:
*   **If $y = 1$:** The second term becomes 0, and the loss simplifies to $L(\hat{y}, y) = -\log(\hat{y})$]. To make this loss small, $\log(\hat{y})$ must be large, which pushes $\hat{y}$ to be as large as possible (close to 1)].
*   **If $y = 0$:** The first term becomes 0, and the loss simplifies to $L(\hat{y}, y) = -\log(1 - \hat{y})$]. To make this loss small, $\log(1 - \hat{y})$ must be large, which pushes $\hat{y}$ to be as small as possible (close to 0)].

## 3. The Cost Function (Entire Dataset)
*   While the Loss function applies to a single example, the **Cost function**, denoted as $J(w, b)$, measures the algorithm's performance over the **entire** training set].
*   It is defined as the average of the loss functions applied to all $m$ training examples]:
$$J(w, b) = \frac{1}{m} \sum_{i=1}^{m} L(\hat{y}^{(i)}, y^{(i)})$$
*   By expanding the loss function, we get the complete formula for the logistic regression cost function]:
$$J(w, b) = -\frac{1}{m} \sum_{i=1}^{m} \left[ y^{(i)} \log(\hat{y}^{(i)}) + (1 - y^{(i)}) \log(1 - \hat{y}^{(i)}) \right]$$
*   **Conclusion:** In training a logistic regression model, our ultimate objective is to find the parameters $w$ and $b$ that minimize this overall cost function $J(w, b)$.
