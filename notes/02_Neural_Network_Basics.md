# 🧠 What is a Neural Network?

## 1. The Simplest Neural Network (A Single Neuron)
To understand a neural network, we can start with a simple Supervised Learning example: predicting the price of a house ($y$) based solely on its size ($x$). 

*   If we use standard linear regression, we fit a straight line to the data. However, house prices can never be negative.
*   To fix this, the function is bent so that it remains at zero for negative values and only rises as a straight line for positive values.
*   This specific mathematical function is called a **ReLU** (Rectified Linear Unit). The term "Rectified" simply means taking the maximum between $0$ and the linear function.
*   A **single neuron** is the simplest possible neural network. It takes an input ($x$), applies this ReLU function, and outputs the estimated price ($y$).

## 2. Building Larger Neural Networks
A larger neural network is formed by taking many of these single neurons and stacking them together, much like stacking Lego bricks.

Instead of predicting the price using only the size, imagine having multiple input features:
*   Size
*   Number of Bedrooms
*   Zip Code (Postal Code)
*   Wealth of the neighborhood

Conceptually, human logic might group these features:
*   *Size* and *#Bedrooms* combine to determine if a house fits a specific **Family Size**.
*   *Zip Code* determines the **Walkability** of the neighborhood.
*   *Zip Code* and *Wealth* combine to determine the **School Quality**.
*   Finally, Family Size, Walkability, and School Quality determine the final **Price**.

## 3. Hidden Layers and Dense Connections
While the conceptual grouping above makes sense to humans, an actual neural network operates differently.

*   When implementing a neural network, you do not manually define what the intermediate nodes (like "Family Size" or "School Quality") represent.
*   You simply provide the raw input features ($x$) and the target output ($y$). The network contains a middle layer called the **Hidden Units**.
*   These hidden units are **densely connected**, meaning every single input feature is connected to every single node in the hidden layer.
*   The neural network is responsible for deciding mathematically what each hidden node should compute based on all the input features provided to it.

## 4. The Core Strength of Neural Networks
*   Neural networks are incredibly powerful in **Supervised Learning** scenarios (mapping an input $x$ to an output $y$).
*   Given enough data (sufficient training examples of $x$ and $y$), neural networks are remarkably effective at automatically figuring out the complex functions that accurately map inputs to outputs.
