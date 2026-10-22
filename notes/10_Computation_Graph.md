# 📊 Computation Graph

## 1. Organizing Neural Network Computations
* The computations of a neural network are strictly organized into two distinct steps:
  1. **Forward Pass (Forward Propagation):** Used to compute the final output of the neural network.
  2. **Backward Pass (Backpropagation):** Used to compute the gradients (derivatives).
* The **computation graph** is a visual tool that explains exactly why the math is organized in this two-step manner.

## 2. Structure of a Computation Graph
* To illustrate how this works, consider a simple function instead of a full neural network: $J(a, b, c) = 3(a + bc)$.
* Computing this function is broken down into three distinct sequential steps (nodes on the graph):
  1. $u = bc$
  2. $v = a + u$
  3. $J = 3v$

## 3. The Forward Pass (Left-to-Right)
* The forward pass moves from left to right across the computation graph to calculate the final output.
* **Example Calculation:** If $a = 5$, $b = 3$, and $c = 2$:
  * Step 1: $u = 3 \times 2 = 6$
  * Step 2: $v = 5 + 6 = 11$
  * Step 3: $J = 3 \times 11 = 33$
* In algorithms like logistic regression, this final distinguished output variable ($J$) represents the **cost function** that we are trying to minimize.

## 4. The Backward Pass (Right-to-Left)
* While the left-to-right pass computes the final value of the cost function $J$, computing the derivatives requires a **right-to-left pass** (moving in the exact opposite direction).
* Moving backward through the graph is the most natural, systematic, and efficient way to calculate all the necessary derivatives for gradient descent.
