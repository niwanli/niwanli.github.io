---
layout: w
title: MIT 1806SC Linear Algebra Session 1.6 - 1.10
date: 2018-03-29
tags:
    - Open Courses
    - Mathematics
    - Linear Algebra
    - MIT 18.06SC Linear Algebra
toc: true

---

Session 1.6: Transpose, Permutation, Vector Spaces $\mathbb{R}^n$
-----------------------------------------------------------------

### Permutations

> Nothing new here.

### Transposes

$$(A^\mathrm{T})_{ij} = A_{ji}$$

<!--more-->

Given any matrix $R$ the product $R^\mathrm{T}R$ is always *symmetric*, which means the transpose of a matrix equals itself, because ($R^\mathrm{T}R)^\mathrm{T} = R^\mathrm{T}(R^\mathrm{T})^\mathrm{T} = R^\mathrm{T}R$.

### Vector spaces

#### Closure

A collection of vectors has to satisfy two conditions:

- closed under addition, which means the sum of any two vectors in the collection lies again in the collection,

- closed under multiplication by any real numbers, that is to say that multiplying any vector in the collection by any real number will not give a vector beyond the collection,

or, to put it in another way, closed under linear combinations.

s.t. we call the collection a *vector space*.

#### Subspaces

A vector space that is contained inside of another vector space is called a *subspace* of that space. For example,

the subspaces of $\mathbb{R}^2$ are:

- all of $\mathbb{R}^2$,
- any line through the zero vector and
- the zero vector alone.

**Every subspace must contain the zero vector.**

#### Column space

Given a matrix $A$, all the linear combinations of the columns of $A$ form a subspace. This is the *column space* $C(A)$.

For example, if $A = \begin{bmatrix}1 & 3 \\ 2 & 3 \\ 4 & 1\end{bmatrix}$, the column space of $A$ is the plane through the origin in $\mathbb{R}^3$ containing $\begin{bmatrix}1 \\ 2 \\ 4\end{bmatrix}$ and $\begin{bmatrix}3 \\ 3 \\ 1\end{bmatrix}$.

------

Session 1.7: Column Space and Nullspace
---------------------------------------

> A typo in both [Problems (PDF)](https://ocw.mit.edu/courses/mathematics/18-06sc-linear-algebra-fall-2011/ax-b-and-the-four-subspaces/column-space-and-nullspace/MIT18_06SCF11_Ses1.6prob.pdf) and [Solutions (PDF)](https://ocw.mit.edu/courses/mathematics/18-06sc-linear-algebra-fall-2011/ax-b-and-the-four-subspaces/column-space-and-nullspace/MIT18_06SCF11_Ses1.6sol.pdf) of this session:
>
> > Problem 6.2: $x - 3y - x = 0$ should be $x -3y - z = 0$.

### Review of subspaces

The union of two subspaces is generally not a subspace, but the intersection of two subspaces is a subspace.

### Column space of $A$ and solving $A\boldsymbol{x} = \boldsymbol{b}$

Given a matrix $A$, the system of linear equations $A\boldsymbol{x} = \boldsymbol{b}$ is solvable exactly when $\boldsymbol{b}$ is a vector in the *column space* of $A$.

### Nullspace of $A$

The *nullspace* of a matrix $A$ is the collection $x$ to the equation $A\boldsymbol{x} = \boldsymbol{0}$.

For example,
$$
\begin{bmatrix}1 & 1 & 2 \\ 2 & 1 & 3 \\ 3 & 1 & 4 \\ 4 & 1 & 5\end{bmatrix}\begin{bmatrix}x_1 \\ x_2 \\ x_3\end{bmatrix} = \begin{bmatrix}0 \\ 0 \\ 0 \\ 0\end{bmatrix},
$$
the nullspace $N(A)$ consists of all multiples of $\begin{bmatrix}1 \\ 1 \\ -1\end{bmatrix}$. This nullspace is a line in $\mathbb{R}^3$.

Attention, a nullspace is a vector space because it obviously satisfies the requirements about addition and scale multiplication. That is to say that any sum or multiple of solutions of $A\boldsymbol{x} = \boldsymbol{0}$ is also a solution: $A(\boldsymbol{x}_1 + \boldsymbol{x}_2) = \boldsymbol{0} + \boldsymbol{0} = \boldsymbol{0}$ and $A(c\boldsymbol{x}) = cA\boldsymbol{x} = c\boldsymbol{0} = \boldsymbol{0}$.

#### Other values of $\boldsymbol{b}$

The solutions to the equation:
$$
\begin{bmatrix}1 & 1 & 2 \\ 2 & 1 & 3 \\ 3 & 1 & 4 \\ 4 & 1 & 5\end{bmatrix}\begin{bmatrix}x_1 \\ x_2 \\ x_3\end{bmatrix} = \begin{bmatrix}1 \\ 2 \\ 3 \\ 4\end{bmatrix},
$$
do not form a subspace. This conclusion is obvious since the zero vector is not a solution to the equation. Actually, the set of solutions forms a line in $\mathbb{R}^3$ that pass through the points $\begin{bmatrix}1 \\ 0 \\ 0\end{bmatrix}$ and $\begin{bmatrix}0 \\ -1 \\ 1\end{bmatrix}$, but not $\begin{bmatrix}0 \\ 0 \\ 0\end{bmatrix}$.

------

Session 1.8:  Solving $A\boldsymbol{x} = \boldsymbol{0}$: Pivot Variables, Special Solutions
--------------------------------------------------------------------------------------------

> A typo in [Solutions (PDF)](https://ocw.mit.edu/courses/mathematics/18-06sc-linear-algebra-fall-2011/ax-b-and-the-four-subspaces/solving-ax-0-pivot-variables-special-solutions/MIT18_06SCF11_Ses1.7sol.pdf) of this session:
>
> > Problem 7.1: $- 23/4$ in rref of $A$ should be $23/4$, and $23/4$ in the solution $\boldsymbol{x}$ should be $-23/4$.

### Computing the nullspace

Just like the way we eliminate the invertible square matrix, we can do the same thing for any matrix $A$.

Suppose:
$$
A = \begin{bmatrix}
1 & 2 & 2 & 2 \\
2 & 4 & 6 & 8\\
3 & 6 & 8 & 10
\end{bmatrix}.
$$
The elimination gives us:
$$
A = \begin{bmatrix}
1 & 2 & 2 & 2 \\
2 & 4 & 6 & 8 \\
3 & 6 & 8 & 10
\end{bmatrix}
\rightarrow
\begin{bmatrix}
1 & 2 & 2 & 2 \\
0 & 0 & 2 & 4 \\
0 & 0 & 2 & 4
\end{bmatrix}
\rightarrow
\begin{bmatrix}
1 & 2 & 2 & 2 \\
0 & 0 & 2 & 4 \\
0 & 0 & 0 & 0
\end{bmatrix}
= U
$$
We call U in *echelon* form. The *rank* of a matrix $A$ is the number of pivots it has. In this example, the rank of $A$ is $2$.

### Special solutions

We can use back-substitution to find the solution $\boldsymbol{x}$ to the equation $U\boldsymbol{x} = \boldsymbol{0}$. In the example, column 1 and 3 are *pivot columns*, column 2 and 4 are *free columns*. We can assign any value to $x_2$ and $x_4$; we call them *free variables*. Yes, $x_1$ and $x_3$ are *pivot variables*.

Suppose $x_2 = 1$ and $x_4 = 0$, then: $x_3 = 0$ and $x_1 = -2$. So that gives us one solution $\boldsymbol{x} = \begin{bmatrix}-2 \\ 1 \\ 0 \\ 0\end{bmatrix}$. Similarly, if $x_2 = 0$ and $x_4 = 1$, then we'll get another solution $\boldsymbol{x} = \begin{bmatrix}2 \\ 0 \\ -2 \\ 1\end{bmatrix}$. **The nullspace of $A$ is the collection of all linear combinations of these "special solution" vectors.**

A fact we should note is that the *rank* of $A$ equals the number of pivot columns, so the number of free columns is the number of columns minus the number of pivot columns, which is also the number of special solution vectors and the dimension of the nullspace.

### Reduced row echelon form

*Reduced row echelon form* (rref form) means pivots equal to 1 and zeros above and below the pivots. Eliminating U gives us a rref form matrix $R$:
$$
U = \begin{bmatrix}
1 & 2 & 2 & 2 \\
0 & 0 & 2 & 4 \\
0 & 0 & 0 & 0
\end{bmatrix}
\rightarrow
\begin{bmatrix}
1 & 2 & 0 & -2 \\
0 & 0 & 2 & 4 \\
0 & 0 & 0 & 0
\end{bmatrix}
\rightarrow
\begin{bmatrix}
1 & 2 & 0 & -2 \\
0 & 0 & 1 & 2 \\
0 & 0 & 0 & 0
\end{bmatrix}
= R.
$$
Generally, $R$ can be rewritten with  a copy of the identity matrix in the upper left corner and some free columns on the right, possibly followed by the lower rows filled with zeros:
$$
R = \begin{bmatrix}
I & F \\
\boldsymbol{0} & \boldsymbol{0}
\end{bmatrix}.
$$
Here $I$ is an $r \times r$ square matrix and $F$ is an $r \times (n - r)$ matrix.

And we can find the nullspace matrix $N = \begin{bmatrix}-F \\ I\end{bmatrix}$ s.t. $RN = \boldsymbol{0}$. Here $I$ is an $(n - r) \times (n - r)$ square matrix and $F$ is an $r \times (n - r)$ matrix. The columns of $N$ are the special solutions.

------

Session 1.9: Solving $A\boldsymbol{x} = \boldsymbol{b}$: Reduced Row Form R
---------------------------------------------------------------------------

### Solvability conditions on $\boldsymbol{b}$

We again the example in the example in the previous session:
$$
A = \begin{bmatrix}
1 & 2 & 2 & 2\\
2 & 4 & 6 & 8\\
3 & 6 & 8 & 10
\end{bmatrix}.
$$
Using Gauss-Jordan elimination:
$$
\left[
\begin{array}{c|c}
\begin{matrix}
1 & 2 & 2 & 2\\
2 & 4 & 6 & 2\\
3 & 6 & 8 &10
\end{matrix}
&
\begin{matrix}
b_1 \\ b_2 \\ b_3
\end{matrix}
\end{array}
\right]
\rightarrow\cdots\rightarrow
\left[
\begin{array}{c|l}
\begin{matrix}
1 & 2 & 2 & 2\\
0 & 0 & 2 & 4 \\
0 & 0 & 0 & 0
\end{matrix}
&
\begin{array}{l}
b_1 \\ b_2 - 2b_1 \\ b_3-b_2-b_1
\end{array}
\end{array}
\right].
$$
In our example, row 3 of $A$ is completely eliminated. So if $A\boldsymbol{x} = \boldsymbol{b}$ has a solution, then $b_3 - b_2 - b_1 = 0$.

From an earlier lecture, we know that $A\boldsymbol{x} = \boldsymbol{b}$ is solvable exactly when $\boldsymbol{b}$ is in the column space $C(A)$. In fact this condition is equivalent with $b_3 - b_2 - b_1 = 0$ here.

### Computing solution

The complete solution is a particular solution plus all the vectors in the nullspace. That is $\boldsymbol{x}_{complete} = \boldsymbol{x}_p + \boldsymbol{x}_n$, where $\boldsymbol{x}_p$ is a particular solution and $\boldsymbol{x}_n$ is a generic vector in the nullspace. To see this, we add $A\boldsymbol{x}_p = \boldsymbol{b}$ to $A\boldsymbol{x}_n = 0$ and get $A(\boldsymbol{x}_p + \boldsymbol{x}_n) = \boldsymbol{b}$ for every vector $\boldsymbol{x}_n$ in the nullspace.

#### A particular solution

For our matrix $A$, we choose $\boldsymbol{b} = \begin{bmatrix}1 \\ 5 \\ 6\end{bmatrix}$, then we get a particular solution $\boldsymbol{x} = \begin{bmatrix}-2 \\ 0 \\ 3/2 \\ 0\end{bmatrix}$ when we let all free variables $x_2$ and $x_4$ equal $0$. (We would get another particular solution when assigning different $x_2$ or $x_4$. This will not affect the complete solution.)

#### Combined with nullspace

From last lecture we learned that the nullspace of $A$ is the collection of all combinations of the special solutions $\begin{bmatrix}-2 \\ 1 \\ 0 \\ 0\end{bmatrix}$ and $\begin{bmatrix}2 \\ 0 \\ -2 \\ 1\end{bmatrix}$. Adding our particular solution to the vectors in the nullspace, we get the complete solution to the equation $A\boldsymbol{x} = \begin{bmatrix}1 \\ 5 \\6\end{bmatrix}$ is:
$$
\boldsymbol{x}_{complete} = \begin{bmatrix}-2 \\ 0 \\ 3/2 \\ 0\end{bmatrix} + c_1 \begin{bmatrix}-2 \\ 1 \\ 0 \\ 0\end{bmatrix} + c_2 \begin{bmatrix}-2 \\ 0 \\ -2 \\ 1\end{bmatrix},
$$
where $c_1$ and $c_2$ are any real numbers.

> A typo in the [lecture summary (PDF)](https://ocw.mit.edu/courses/mathematics/18-06sc-linear-algebra-fall-2011/ax-b-and-the-four-subspaces/solving-ax-b-row-reduced-form-r/MIT18_06SCF11_Ses1.8sum.pdf) of this session:
>
> > $c_1$ is missing here...

The nullspace is a two dimensional subspace of $\mathbb{R}^4$, and the complete solution form a plane parallel to that through $\boldsymbol{x}_p = \begin{bmatrix}-2 \\ 0 \\ 3/2 \\ 0\end{bmatrix}$.

### Rank

The rank of a matrix equals the number of pivots of that matrix. If $A$ is an $m$ by $n$ matrix of rank $r$, we know $r \le m$ and $r \le n$. Actually the rank tells us all the information about solutions to the equation $A\boldsymbol{x} = \boldsymbol{b}$.
$$
\begin{array}{|c|c|c|c|c|}
\hline
& r = m = n & r = n < m & r = m < n & r < m, r < n \\
\hline
R & I & \begin{bmatrix}I \\ \boldsymbol{0}\end{bmatrix} & \begin{bmatrix}I & F\end{bmatrix} & \begin{bmatrix}I & F \\ \boldsymbol{0} & \boldsymbol{0}\end{bmatrix} \\
\hline
\text{Solutions to }A\boldsymbol{x} = \boldsymbol{b} & 1 & 0\text{ or }1 & \infty & 0\text{ or }\infty \\
\hline
\end{array}
$$

------

Session 1.10: Independence, Basis and dimension
-----------------------------------------------

### Linear Independence

$\sum_i c_i\boldsymbol{x}_i = \boldsymbol{0}$ only when $c_1, c_2, \dots, c_n$ are all $0$.

$\Leftrightarrow$ The only solution to $A\boldsymbol{x} = \boldsymbol{0}$ is $\boldsymbol{x} = \boldsymbol{0}$, which means that the nullspace of $A$ contains only the zero vector.

$\Leftrightarrow$ The rank of $A$ is $n$ so there are no free variables.

### Spanning a space

Vectors $\boldsymbol{v}_1, \boldsymbol{v}_2, \dots, \boldsymbol{v}_k$ *span* a space when the space consists of all combinations of those vectors. The space spanned is also the smallest space containing those vectors.

### Basis and dimension

A *basis* for a vector space is a sequence of vectors $\boldsymbol{v}_1, \boldsymbol{v}_2, \dots, \boldsymbol{v}_d$ with two properties:

- $\boldsymbol{v}_1, \boldsymbol{v}_2, \dots, \boldsymbol{v}_d$ are independent;
- $\boldsymbol{v}_1, \boldsymbol{v}_2, \dots, \boldsymbol{v}_d$ span the vector space.

The number of vectors in a basis for a vector space is the *dimension* of the space. There are exactly $n$ vectors in every basis for $\mathbb{R}^n$.

### Basis of a column space and nullspace

$$\text{dimension of }C(A)  = \text{number of pivot columns of }A = \text{rank}(A)$$

$$\text{dimension of }N(A)  = \text{number of free variables of }A = \text{number of columns of }A - \text{rank}(A)$$

-------

**LICENSE**:

This work is built upon the materials on [MIT OCW](https://ocw.mit.edu/courses/mathematics/18-06sc-linear-algebra-fall-2011/index.htm).

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.