# 🧮 Binary Classification and Notation

## 1. Binary Classification Basics
*   Logistic regression is an algorithm specifically designed for **binary classification**.
*   The primary goal is to learn a function that maps an input feature vector $x$ to an output label $y$, where $y$ is either $0$ or $1$ ($y \in \{0, 1\}$).
*   **Example:** In a computer vision problem where the goal is to build a "Cat Recognizer," an output of $y=1$ indicates a cat, and $y=0$ indicates a non-cat.

## 2. Image Representation and "Unrolling"
*   Computers store images as three separate matrices corresponding to the Red, Green, and Blue (RGB) color channels. For a $64 \times 64$ pixel image, there are three $64 \times 64$ matrices.
*   **Unrolling:** To feed this image into a neural network, all the pixel intensity values across these three matrices are "unrolled" into a single, long 1-dimensional column vector named $x$.
*   **Input Dimension ($n_x$):** The total dimension of this input feature vector is denoted as $n_x$ (or sometimes just $n$). For a $64 \times 64$ image, the dimension is calculated as:
    $$n_x = 64 \times 64 \times 3 = 12,288$$

## 3. Standard Mathematical Notation
Throughout deep learning literature and implementations, the following notation is universally standard:
*   **$(x, y)$:** Represents a single training example.
*   **$x \in \mathbb{R}^{n_x}$:** The input feature is a vector with $n_x$ dimensions.
*   **$y \in \{0, 1\}$:** The target label is a binary value.
*   **$m$:** The total number of training examples in the dataset (sometimes written as $m_{train}$). Similarly, $m_{test}$ denotes the number of testing examples.
*   **Superscripts $(i)$:** The notation $(x^{(i)}, y^{(i)})$ denotes the $i$-th specific training example in the dataset. *(Do not confuse this with exponents)*.

## 4. Data Matrices ($X$ and $Y$)
To process a massive training set efficiently without using slow explicit `for` loops, deep learning organizes the data into matrices.

### The Input Matrix ($X$)
*   In deep learning, instead of stacking training examples in rows, we stack the input vectors $x^{(1)}, x^{(2)}, \dots, x^{(m)}$ side-by-side in **columns**.
*   This creates a matrix $X$ with $n_x$ rows and $m$ columns.

$$X = \begin{bmatrix} 
| & | & & | \\ 
x^{(1)} & x^{(2)} & \dots & x^{(m)} \\ 
| & | & & | 
\end{bmatrix}$$

*   Mathematically, $X \in \mathbb{R}^{n_x \times m}$. 
*   In Python (using NumPy), running `X.shape` will output `(n_x, m)`.

### The Output Matrix ($Y$)
*   Similarly, the output labels $y^{(1)}, y^{(2)}, \dots, y^{(m)}$ are stacked side-by-side in columns.
*   This creates a matrix $Y$ with $1$ row and $m$ columns.

$$Y = \begin{bmatrix} y^{(1)} & y^{(2)} & \dots & y^{(m)} \end{bmatrix}$$

*   Mathematically, $Y \in \mathbb{R}^{1 \times m}$.
*   In Python, running `Y.shape` will output `(1, m)`.
