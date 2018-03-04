---
layout: post
title:  "Yandex School of Data Analysis Part 2. Linear Algebra"
date:   2015-05-16 12:45:01
external: [latex]
---

In this post I continue to share the answers to the Yandex School of Data Analysis 2015 sanity test. I worked through the first set of problems in my <a href="{{ page.previous.url | prepend: site.baseurl }}" title="{{ page.previous.title }}">previous post</a>. In this post I am looking at the linear algebra problems offered in the test. For each problem I give the answer I submitted and explain how I got it. I'm using [Maxima](http://maxima.sourceforge.net) 5.34.1 to check myself.

<!--more-->

####__D. Eigenvector__
Find an eigenvector of the matrix A

$$
\left(\begin{array}{ccc}
6 & -2 & 2\\
-2 & 5 & 0\\
2 & 0 & 7\\
\end{array}\right)
$$

that corresponds to its biggest eigenvalue.

__Answer.__  $(1, -0.5, 1)$

__Solution.__  First, we find all eigenvalues $\lambda$.

$$
det(A - \lambda I) = det
\begin{bmatrix}
6-\lambda & -2 & 2\\
-2 & 5-\lambda & 0\\
2 & 0 & 7-\lambda\\
\end{bmatrix} = (6-\lambda)(\lambda-3)(\lambda-9) = 0
$$

$$
\lambda_1 = 6, \; \lambda_2 = 3, \; \lambda_3 = 9
$$

The biggest eigenvalue is 9. Then we find the corresponding eigenvectors:

$$
Ax = 9x
$$

$$
\left(\begin{array}{ccc}
6 & -2 & 2\\
-2 & 5 & 0\\
2 & 0 & 7\\
\end{array}\right) \left(\begin{array}{c}
x_1\\
x_2\\
x_3\\
\end{array}\right) = 9 \left(\begin{array}{c}
x_1\\
x_2\\
x_3\\
\end{array}\right) 
$$

$$
\begin{cases}
6x_1 -2x_2 + 2x_3 = 9 x_1\\
-2x_1 + 5x_2 = 9 x_2\\
2x_1 + 7x_3 = 9 x_3\\
\end{cases}
$$

$$
\begin{cases}
3x_1 + 2x_2 - 2x_3 = 0\\
x_1 + 2x_2 = 0\\
x_1 - x_3 = 0\\
\end{cases}
$$

$$
x_3 = x_1, \; x_2 = -\frac{1}{2} x_1
$$

Setting $x_1 = 1$ we get $(1, 0.5, 1)$.

Maxima code:
{% highlight ruby %}
eivects(matrix([6,-2,2],[-2,5,0],[2,0,7]));
#=>[[[3, 9, 6], [1, 1, 1]], [[[1, 1, - 0.5]], [[1, - 0.5, 1]], [[1, - 2, - 2]]]]
{% endhighlight %}

The first element of the list $[[3, 9, 6], [1, 1, 1]]$ is a list of the eigenvalues of A and a list of the multiplicities of the eigenvalues. The second is a list of lists of eigenvectors that correspond to each eigenvalue.


####__E. Parametrized matrix__
Find $a$ for which the matrix

$$
\left(\begin{array}{ccc}
a-1 & a-1 & a(a-1)\\
2a-3 & 3a-5 & a^2-2\\
-1 & a-3 & 4a-5\\
\end{array}\right)
$$

has rank 2.

__Answer.__  $a=1$ and $a=2$

__Solution.__  The rank of a matrix is the maximum number of linearly independent rows (columns) of the matrix. Two rows $x=[x_1 \; x_2 \; \dots \; x_n]$ and $y=[y_1 \; y_2 \; \dots \; y_n]$ are linearly dependent if there exists the scalar $t \ne 0$, such that $x + yt = 0$.

The given matrix has rank 2 if and only if exactly two of its rows are linearly dependent. Then, the following 3 cases are possible:

* The first row and the second row are linearly dependent

$$
\begin{cases}
a-1 + t(2a-3) = 0\\
a-1 + t(3a-5) = 0\\
a(a-1) + t(a^2-2) = 0\\
\end{cases}
$$

Maxima code:
{% highlight ruby %}
solve([a-1+t*(2*a-3)=0, a-1+t*(3*a-5)=0, a*(a-1)+t*(a^2-2)=0], [a, t]);
#=> [[a = 2, t = - 1], [a = 1, t = 0]]
{% endhighlight %}

$$
a=2, \; t=-1
$$

The matrix turns

$$
\begin{bmatrix}
1 & 1 & 2\\
1 & 1 & 2\\
-1 & -1 & 3\\
\end{bmatrix}
$$.

* The second row and the third row are linearly dependent

$$
\begin{cases}
2a-3 - t = 0\\
3a-5 + t(a-3) = 0\\
a^2-2 + t(4a-5) = 0\\
\end{cases}
$$

Maxima code:
{% highlight ruby %}
solve([2*a-3-t=0, 3*a-5+t*(a-3)=0, a^2-2+t*(4*a-5)=0], [a, t]);
#=>[[a = 1, t = - 1]]
{% endhighlight %}

$$
a=1, \; t=-1
$$

The matrix turns

$$
\begin{bmatrix}
0 & 0 & 0\\
-1 & -2 & -1\\
-1 & -2 & -1\\
\end{bmatrix}
$$.

* The first row and the third row are linearly dependent

$$
\begin{cases}
a-1 - t =0\\
a-1 + t(a-3) = 0\\
a(a-1) + t(4a-5) = 0\\
\end{cases}
$$

Maxima code:
{% highlight ruby %}
solve([a-1-t=0, a-1+t*(a-3)=0, a*(a-1)+t*(4*a-5)=0], [a, t]);
#=>[[a = 1, t = 0]]
{% endhighlight %}
No solution with $t \ne 0$.
