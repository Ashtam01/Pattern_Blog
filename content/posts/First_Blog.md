---
title: "Minimising Manhattan Distance"
date: 2025-10-19
math: true
description: "Exploring Manhattan, a lesser-discussed metric compared to its Euclidean counterpart"
tags: ["Algorithms", "Competitive Programming", "Math"]
---

Unlike the more familiar Euclidean distance, which measures the straight-line path, the Manhattan distance calculates the length of the shortest path restricted to **axis-aligned movements**.


## Definition: L1 Norm


In mathematics, the Manhattan distance, also known as the **L1 norm** or $\ell_1$ norm, is part of the Minkowski distance family. It is calculated by summing the absolute differences between the coordinates of two points in space.

For two points in an $n$-dimensional space, defined as:
- $\mathbf{a} = (a_1, a_2, \dots, a_n)$
- $\mathbf{b} = (b_1, b_2, \dots, b_n)$

The Manhattan distance, denoted $d_1(\mathbf{a}, \mathbf{b})$, is given by:

$$ d_1(\mathbf{a}, \mathbf{b}) = |\mathbf{a} - \mathbf{b}\| = \sum_{i=1}^{n} |a_i - b_i| $$

This distance qualifies as a true **metric** because it satisfies the four essential properties of a metric space:

1. **Non-negativity**: The distance is always zero or positive.
   $$ d_1(\mathbf{a}, \mathbf{b}) \geq 0 $$

2. **Identity of indiscernibles**: The distance is zero only when the points are identical.
   $$ d_1(\mathbf{a}, \mathbf{b}) = 0 \iff \mathbf{a} = \mathbf{b} $$

3. **Symmetry**: The distance from $\mathbf{a}$ to $\mathbf{b}$ equals the distance from $\mathbf{b}$ to $\mathbf{a}$.
   $$ d_1(\mathbf{a}, \mathbf{b}) = d_1(\mathbf{b}, \mathbf{a}) $$

4. **Triangle Inequality**: For any point $\mathbf{c}$, the direct distance between $\mathbf{a}$ and $\mathbf{b}$ is less than or equal to the sum of distances through $\mathbf{c}$.
   $$ d_1(\mathbf{a}, \mathbf{b}) \leq d_1(\mathbf{a}, \mathbf{c}) + d_1(\mathbf{c}, \mathbf{b}) $$

By fulfilling these properties, particularly the triangle inequality, the Manhattan distance serves as a consistent and dependable metric for numerous optimization techniques.

## Which point minimizes the L1 norm?



The key to solving the multi-dimensional minimization problem is the **separability principle**. The formula for the total Manhattan distance from a candidate point $\mathbf{x} = (x, y, \dots)$ to a set of $n$ points $\mathbf{p_i} = (p_{i,x}, p_{i,y}, \dots)$ can be decomposed:

$$
D(\mathbf{x}) = \sum_{i=1}^{n} d_1(\mathbf{p_i}, \mathbf{x}) = \sum_{i=1}^{n} \left( |p_{i,x} - x| + |p_{i,y} - y| \right)+ \dots
$$

This sum can be rearranged as:

$$
D(\mathbf{x}) = \left( \sum_{i=1}^{n} |p_{i,x} - x| \right) + \left( \sum_{i=1}^{n} |p_{i,y} - y| \right) + \dots
$$

This decomposition shows that the total distance is simply the sum of several independent one-dimensional problems. To minimize the total distance $D(\mathbf{x})$, one can minimize each dimensional sum separately.


Due to the separability principle, the entire problem boils down to solving the following one-dimensional case:

Given a set of $n$ points $p_1, p_2, \dots, p_n$ on a line, find a point $x$ that minimizes the sum of absolute deviations:

$$f(x) = \sum_{i=1}^{n} |p_i - x|$$



**Theorem :** The point $x$ that minimizes the sum of absolute deviations $f(x)$ is the **median** of the set of points $p_1, \dots, p_n$.




## Proof

To prove this theorem, we can analyze the properties of the function $f(x)$. The absolute value function, $|a|$, is a convex function. Since $f(x)$ is a sum of convex functions, $f(x)$ itself is also a convex function.

For a convex function, the global minimum occurs at any point $x$ where the derivative (or more precisely, the subgradient) is zero.

### The Subgradient Approach

The absolute value function $f(u) = |u|$ has a sharp corner at $u=0$, so it's not differentiable at that one point. However, we can analyze its derivative for all other points.

Let's look at the derivative of a single term $|p_i - x|$ with respect to $x$:

* If $x < p_i$, the expression is $(p_i - x)$, and its derivative is $-1$.
* If $x > p_i$, the expression is $(x - p_i)$, and its derivative is $+1$.

We can write this using the sign function, $\text{sign}(u)$, which is $-1$ for negative numbers and $+1$ for positive numbers. The derivative of $|p_i - x|$ with respect to $x$ is simply $\text{sign}(x - p_i)$.

By the sum rule of differentiation, the derivative of our total function $f(x)$ is the sum of the individual derivatives:

$$f'(x) = \sum_{i=1}^{n} \text{sign}(x - p_i)$$

To find the minimum, we set this derivative to zero:

$$f'(x) = \sum_{i=1}^{n} \text{sign}(x - p_i) = 0$$

This equation can be interpreted simply: $\text{sign}(x - p_i)$ adds a $+1$ for every point $p_i$ that is to the left of $x$ (since $x > p_i$) and a $-1$ for every point $p_i$ that is to the right of $x$ (since $x < p_i$).

Therefore, $f'(x) = 0$ means:

$$(\text{Number of points to the left of } x) - (\text{Number of points to the right of } x) = 0$$

This is only true when the number of points on either side of $x$ is equal. This is precisely the definition of the **median**.

### Handling Odd and Even Cases

The nature of the solution depends on whether $n$ (the number of points) is odd or even. Let's assume the points are sorted: $p_1 \le p_2 \le \dots \le p_n$.

* **Case 1: $n$ is odd**
    Let $n = 2k + 1$. The unique median is the middle point, $p_{k+1}$.
    * If we pick an $x$ slightly to the left of $p_{k+1}$, there are $k$ points to the left and $k+1$ points to the right. The derivative $f'(x)$ will be $k - (k+1) = -1$, meaning the function is decreasing.
    * If we pick an $x$ slightly to the right of $p_{k+1}$, there are $k+1$ points to the left and $k$ points to the right. The derivative $f'(x)$ will be $(k+1) - k = +1$, meaning the function is increasing.
    Since the function decreases until it hits $p_{k+1}$ and increases after, **the minimum is uniquely at $x = p_{k+1}$**.

* **Case 2: $n$ is even**
    Let $n = 2k$. Any point between the two middle elements, $p_k$ and $p_{k+1}$, is a valid median.
    * If we pick an $x$ anywhere in the open interval $(p_k, p_{k+1})$, there are $k$ points to the left ($p_1 \dots p_k$) and $k$ points to the right ($p_{k+1} \dots p_{2k}$).
    * The derivative $f'(x)$ is $k - k = 0$ for the entire interval. This means the function $f(x)$ is **constant (flat)** between $p_k$ and $p_{k+1}$.
    Any $x$ within the closed interval $[p_k, p_{k+1}]$ minimizes the sum. This means **the solution is not unique**.
## Weighted Median : A Variant


Given a set of $n$ points $\{p_1, \dots, p_n\}$ with corresponding positive weights $\{w_1, \dots, w_n\}$, the goal is to find a point $x$ that minimizes the weighted sum of absolute deviations:

$$ g(x) = \sum_{i=1}^n w_i |p_i - x| $$

The solution to this problem is the **weighted median**. A point $p_k$ is a weighted median if it satisfies the following conditions, where $W(\text{total}) = \sum_{i=1}^n w_i$ :

$$ \sum_{p_i < p_k} w_i \le \frac{W(\text{total})}{2} \quad \text{and} \quad \sum_{p_i > p_k} w_i \le \frac{W(\text{total})}{2} $$

Essentially, the weighted median is the point that partitions the total weight of the set into two halves as equally as possible.

### Proof

The point $x*$ that minimizes $g(x) = \sum_{i=1}^n w_i |p_i - x|$ is the weighted median of the set of points.

The derivative of $g(x)$ with respect to $x*$ is:

$$ g'(x) = \sum_{i=1}^n w_i \cdot \text{sgn}(x - p_i) $$

This can be rewritten as the difference between the sum of weights for points to the left of $x*$ and the sum of weights for points to the right of $x*$:

$$ g'(x) = \sum_{p_i < x} w_i - \sum_{p_i > x} w_i $$

The minimum of the convex function $g(x)$ occurs where its derivative (or subgradient) is zero. Setting $g'(x) = 0$ gives the condition:

$$ \sum_{p_i < x} w_i = \sum_{p_i > x} w_i $$

This is the "pseudo-halving property" which defines the balance point of the weights. $^{23}$ A

> more formal proof analyzes the slopes of the piecewise linear function $g(x)$. $^{24}$ The slope in the interval between sorted points $p_{(i)}$ and $p_{(i+1)}$ is given by $2 \cdot \left(\sum_{i=1}^j w_{(i)}\right) - W(\text{total})$. The minimum must occur where this slope transitions from negative to non-negative, which is precisely at the point(s) satisfying the definition of the weighted median.

This demonstrates that the median is not just a point that balances the count of data points, but more generally, a point that balances their influence or weight. The unweighted median is simply a special case where all points are assigned equal weight.
## Practice Problems
Here, I have listed some problems using this same property. Try to solve them by yourselves, although I have included solutions in Cpp.

1. [Codeforces](https://codeforces.com/contest/2149/problem/D)
2. [Leetcode 462](https://leetcode.com/problems/minimum-moves-to-equal-array-elements-ii/description/)
3. [Leetcode 2448](https://leetcode.com/problems/minimum-cost-to-make-array-equal/description/)
4. [Codeforces](https://codeforces.com/problemset/problem/99/B)
5. [Leetcode 2134](https://leetcode.com/problems/minimum-swaps-to-group-all-1s-together-ii/description/)
6. [Codeforces](https://codeforces.com/problemset/problem/1406/D)
7. [CSES](https://cses.fi/problemset/task/1674)





