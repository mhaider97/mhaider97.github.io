---
title: "NumPy Crash Course: A Quick Guide for Beginners"
date: 2025-09-04
categories: [Data Science]
tags: [Python, Numpy]
---

If you’re diving into data science, machine learning, or scientific computing in Python, **NumPy** is your best friend. It’s the foundation of Python’s data ecosystem, and mastering it will save you hours of coding time.

In this crash course, we’ll walk through the essentials of NumPy with simple explanations and examples.

## What is NumPy?
NumPy (Numerical Python) is a library for working with arrays, matrices, and mathematical functions.

Why NumPy?
- Faster than Python lists (written in C).
- Uses less memory.
- Supports vectorized operations.
- Works seamlessly with libraries like Pandas, Scikit-learn, and TensorFlow.

## Getting Started
```bash
# Install NumPy (if not already installed)
pip install numpy
```
```python
# Import convention
import numpy as np
```

## Creating Arrays
```python
# From list
arr = np.array([1, 2, 3, 4]) # converts a Python list into a NumPy array
print(arr)

# Zeros, Ones, Full, Identity
print(np.zeros((2, 3))) # creates a 2x3 array filled with 0s
print(np.ones((2, 3))) # creates a 2x3 array filled with 1s
print(np.full((2, 2), 7)) # creates a 2x2 array filled with a specific value
print(np.eye(3))  # creates a 3x3 identity matrix (diagonal of 1s, rest 0s)

# Ranges
print(np.arange(0, 10, 2)) # generates values with a step (like Python’s range)
print(np.linspace(0, 1, 5)) # generates evenly spaced values between two limits

# Random
print(np.random.rand(2, 2)) # gives random numbers between 0 and 1
print(np.random.randn(2, 2)) # gives random numbers from a standard normal distribution
print(np.random.randint(1, 10, 5)) # generates random integers within a range
```

> These NumPy methods are essential building blocks for **data manipulation and numerical computing**. Functions like zeros, ones, and full are handy for initializing arrays, while arange and linspace help generate sequences for simulations or plotting. Random array generators are widely used in machine learning, testing, and statistical modeling.

## Array Basics
```python
a = np.array([[1, 2, 3], [4, 5, 6]]) # Creates a 2D array (2 rows, 3 columns)
print(a.shape) # Gives the dimensions of the array -> 2 rows, 3 columns
print(a.size) # Returns the total number of elements in the array
print(a.dtype) # Shows the data type of array elements (e.g., int64, float32)

# Reshape
print(a.reshape(3, 2)) # Changes the shape of the array to 3 rows and 2 columns

# Flatten
print(a.ravel()) # Flattens the array into a 1D array

# Indexing
print(a[0, 1]) # Accesses the element at row 0, column 1 -> value 2
print(a[:, 1]) # Selects the entire second column of the array

# Boolean indexing
print(a[a > 3]) # Returns elements that satisfy a condition (all values greater than 3)
```

> Array properties **(shape, size, dtype)** make it easy to inspect data, and reshaping or flattening is crucial when preparing inputs for models or algorithms. Indexing and boolean indexing allow precise data selection and filtering, which is especially useful in data analysis, preprocessing, and working with large datasets.

## Mathematical Operations
```python
x = np.array([1, 2, 3])
y = np.array([4, 5, 6])

# Element-wise operations on arrays x and y
print(x + y)
print(x * y)
print(x ** 2)

# Broadcasting
m = np.ones((3, 3)) # Adds a scalar (5) to every element of the matrix using broadcasting
print(m + 5)

# Aggregations
print(np.sum(x)) # Computes the sum of all elements
print(np.mean(x)) # Finds the average (mean) of the elements
print(np.std(x)) # Calculates the standard deviation (measure of spread)
print(np.min(x), np.max(x)) # Finds the minimum and maximum values
print(np.argmin(x), np.argmax(x)) # Returns the indices of min and max values

# Matrix multiplication 
# Both perform dot product -> here, 1*4 + 2*5 + 3*6 = 32
print(np.dot(x, y))
print(x @ y)
```

> These operations are at the core of scientific computing and data analysis with NumPy. Element wise arithmetic and broadcasting make it easy to perform fast calculations without writing loops, which is especially useful in numerical simulations, feature engineering, and image processing. Aggregation functions like sum, mean, and std provide quick insights into datasets, making them essential for statistics and exploratory data analysis. Matrix multiplication (dot or @) is widely used in linear algebra, powering applications such as machine learning algorithms, neural networks, and recommendation systems. Together, these methods form the foundation for efficient numerical workflows in Python.

Curious about mean and standard deviation? Dive into the articles below to master them in minutes!
- [Mean and Median of Matrix](https://www.geeksforgeeks.org/dsa/mean-median-matrix/)
- [Variance and Standard Deviation](https://www.geeksforgeeks.org/dsa/variance-standard-deviation-matrix/)

## Useful Array Functions
```python
arr = np.array([3, 1, 2, 5, 4])

print(np.sort(arr)) # Sorts the array in ascending order
print(np.argsort(arr)) # Returns the indices that would sort the array

# Concatenation
a = np.array([1, 2])
b = np.array([3, 4])
print(np.concatenate([a, b])) # Joins arrays into a single array -> [1 2 3 4]

# Stack
print(np.vstack([a, b])) # Vertical stack (row-wise) -> creates a 2D array
print(np.hstack([a, b])) # Horizontal stack (column-wise) -> merges into one row

# Split
c = np.array([1, 2, 3, 4, 5, 6])
print(np.split(c, 3)) # Splits array into equal parts -> 3 sub-arrays

# Unique
print(np.unique([1, 2, 2, 3, 3, 3])) # Returns the unique elements -> [1 2 3]

# Copy vs View
arr1 = np.array([1, 2, 3])
arr2 = arr1.view() # creates a shallow copy (changes in one affect the other)
arr3 = arr1.copy() # creates a deep copy (completely independent array)
```

> These methods are especially useful when working with structured or large datasets. Sorting and argsort are key for ranking, ordering, and searching operations. Concatenation and stacking allow combining data from multiple sources, while splitting helps in dividing datasets into smaller chunks for training, testing, or batch processing. unique is often used to identify distinct categories or remove duplicates in data analysis. Finally, understanding the difference between view and copy is crucial for memory management view provides efficiency when working with large arrays, while copy ensures data safety when independent modifications are needed.

## Linear Algebra
```python
M = np.array([[1, 2], [3, 4]])

print(np.linalg.det(M)) # Computes the determinant of the matrix
print(np.linalg.inv(M)) # Finds the inverse of the matrix (if it exists)

vals, vecs = np.linalg.eig(M)
print(vals) # Eigenvalues represent scaling factors of the transformation
print(vecs) # Eigenvectors represent directions that remain unchanged after the transformation
```

> These linear algebra functions are widely used in scientific computing, physics, and machine learning. Determinants and inverses are fundamental in solving linear systems, while eigenvalues and eigenvectors play a crucial role in dimensionality reduction techniques like PCA, stability analysis, and understanding transformations in vector spaces.

Confused by linear algebra terms? The articles below break down Determinant, Inverse, Eigenvectors, and Eigenvalues in a simple, practical way
- [Determinant of Matrix](https://www.geeksforgeeks.org/maths/what-is-determinant-of-a-matrix/)
- [Inverse of Matrix](https://www.geeksforgeeks.org/maths/inverse-of-matrix/)
- [Eigen Values](https://www.geeksforgeeks.org/engineering-mathematics/eigen-values/)

## Practical Examples
### Create Linear DataSet
Your goal is to create a simple dataset consisting of a single feature and a label as follows:

1. Assign a sequence of integers from 6 to 20 (inclusive) to a NumPy array named feature.
2. Assign 15 values to a NumPy array named label such that:

```python
feature = np.arange(6, 21)
print("Feature: ", feature)

label = (feature * 3) + 4
print("Label: ", label)
```

### Add Some Noise to the Dataset
To make your dataset a little more realistic, insert a little random noise into each element 
of the label array you already created. To be more precise, modify each value assigned to 
label by adding a different random floating-point value between -2 and +2.

Don't rely on broadcasting. Instead, create a noise array having the same dimension as label.
```python
noise = (np.random.random([15]) * 4) - 2
print("Noise: ", noise)

label = label + noise
print("Label: ", label)
```

## Performance: Why NumPy is Fast
- Written in C for speed.
- Avoids Python loops by vectorization.
- Uses less memory.

```python
import time

n = 10**6
list1 = list(range(n))
list2 = list(range(n))

# Python loop
start = time.time()
result = [list1[i] + list2[i] for i in range(n)]
print("Python loop:", time.time() - start)

# NumPy vectorized
arr1 = np.arange(n)
arr2 = np.arange(n)
start = time.time()
result = arr1 + arr2
print("NumPy vectorized:", time.time() - start)
```

> This example highlights the performance difference between plain Python loops and NumPy’s vectorized operations. Using a Python list comprehension to add two large lists element wise takes significantly more time because it processes elements one by one in pure Python. In contrast, NumPy leverages optimized C-based implementations under the hood, allowing the same operation (arr1 + arr2) to run much faster. This showcases why NumPy is the go to choice for numerical computing and handling large datasets efficiently.

## Conclusion
NumPy is the backbone of scientific computing in Python. Once you’re comfortable with arrays, indexing, and vectorized operations, you’ll find it much easier to move into Pandas, Matplotlib, and Scikit-learn.

Next steps:
- Pandas for data manipulation
- Matplotlib/Seaborn for visualization
- Scikit-learn for machine learning

## Links
- [Github Repo](https://github.com/mhaider97/experiments/blob/main/numpy_practice.py)
- [NumPy Google Colab](https://colab.research.google.com/github/google/eng-edu/blob/main/ml/cc/exercises/numpy_ultraquick_tutorial.ipynb)
- [NumPy Docs](https://numpy.org/doc/2.3/user/absolute_beginners.html)
- [Geeksforgeeks](https://www.geeksforgeeks.org/)