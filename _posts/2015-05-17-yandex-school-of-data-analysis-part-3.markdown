---
layout: post
title:  "Yandex School of Data Analysis Part 3. Combinatorics and Probability"
date:   2015-05-17 18:30:04
external: [latex]
---

This is part 3.

####__F. Permutations__
Find the total number of inversions in the permutation \( X \), where
`\[
A \: X \: B = C
\]`
`\[
A = \left(\begin{array}{ccccccc}
1 & 2 & 3 & 4 & 5 & 6 & 7\\
2 & 7 & 5 & 4 & 6 & 1 & 3\\
\end{array}\right)
\]`
`\[
B = \left(\begin{array}{ccccccc}
1 & 2 & 3 & 4 & 5 & 6 & 7\\
1 & 4 & 7 & 3 & 6 & 5 & 2\\
\end{array}\right)
\]`
`\[
C = \left(\begin{array}{ccccccc}
1 & 2 & 3 & 4 & 5 & 6 & 7\\
5 & 6 & 2 & 1 & 7 & 4 & 3\\
\end{array}\right)
\]`
The rightmost permutation is applied first.

__Answer.__  17

__Solution.__  We denote the permutation of the element `\( n \)` in the set permutation `\( \varphi \)` as `\( \varphi (n) \)`. Then
`\[
A(1)=2, \; A(2)=7, \; A(3)=5, \; A(4)=4, \; A(5)=6, \; A(6)=1, \; A(7)=3.
\]`

Similarly,
`\[
B(1)=1, \; B(2)=4, \; B(3)=7, \; B(4)=3, \; B(5)=6, \; B(6)=5, \; B(7)=2
\]`
and
`\[
C(1)=5, \; C(2)=6, \; C(3)=2, \; C(4)=1, \; C(5)=7, \; C(6)=4, \; C(7)=3.
\]`

Let `\( X(1)=x_1, \; X(2)=x_2, \; X(3)=x_3, \; X(4)=x_4, \;X(5)=x_5, \; X(6)=x_6 \)` and `\( X(7)=x_7 \)`. Then for each element `\( n \)` in `\( (1,2,3,4,5,6,7) \)`   `\( A(X(B(n)))=C(n) \)`.
`\[
\begin{align}
A(X(B(1)))&=A(X(1))=A(x_1)=5, \; x_1=3\\
A(X(B(2)))&=A(X(4))=A(x_4)=6, \; x_4=5\\
A(X(B(3)))&=A(X(7))=A(x_7)=2, \; x_7=1\\
A(X(B(4)))&=A(X(3))=A(x_3)=1, \; x_3=6\\
A(X(B(5)))&=A(X(6))=A(x_6)=7, \; x_6=2\\
A(X(B(6)))&=A(X(5))=A(x_5)=4, \; x_5=4\\
A(X(B(7)))&=A(X(2))=A(x_2)=3, \; x_2=7
\end{align}
\]`

Thus, `\( X = \left(\begin{array}{ccccccc}
1 & 2 & 3 & 4 & 5 & 6 & 7\\
3 & 7 & 6 & 5 & 4 & 2 & 1\\
\end{array}\right) \)`.

The following python code evaluates the product of the permutations `\(A, \; X\)` and `\(B\)`, and checks the result against `\(C.\)` Then it calculates the total number of inversions in `\(X.\)`
{% highlight python %}
import itertools

def inversion_number(A):
    return sum(1 for x,y in itertools.combinations(xrange(len(A)),2) if A[x]>A[y])

def product(A,X,B):
    return [A[ X[ B[i]-1 ]-1 ] for i in xrange(len(A))]

A = [2,7,5,4,6,1,3]
X = [3,7,6,5,4,2,1]
B = [1,4,7,3,6,5,2]
C = [5,6,2,1,7,4,3]

R = product(A,X,B)
assert(C == R)
print inversion_number(X)
#=> 17
{% endhighlight %}


####__G. Toy soldiers__
Gene has 6 red, 3 blue and 4 green toy soldiers and he wants to put them in a row so that there are no green soldiers who follow each other. How many ways is there to do so? The soldiers of the same color are not distinguishable.

__Answer.__  17640

__Solution.__ First, we put all red and blue soldiers in a row leaving some space between them. This can be done in `\( C_{6+3}^{3} = C_{6+3}^{6} = \frac{9!}{3! \cdot 6!} \)` ways. Now as we want green soldiers not to follow each other, we can put any green soldier in any place between the two soldiers in the row. The row has 9 soldiers in it, hence there are `\( 8+2=10\)` places for green soldiers (a place before the first soldier, 8 places between the soldiers and a place after the last soldier). The 4 green soldiers can be put in 10 places in `\( C_{10}^{4}=\frac{10!}{4! \cdot 6!} \)` ways. Gene can do what he wants in
`\[
\frac{9!}{3! \cdot 6!} \cdot \frac{10!}{4! \cdot 6!} = 17640
\]`
ways.


####__H. Blue Oaks__
`\( \frac{3}{4} \)` of all trains that pass the Blue Oaks station everyday are passenger trains, and others are freight trains. On average 20% of passenger trains and 5% of freight trains stop there. Find the probability that a passing train makes a stop at Blue Oaks.

__Answer.__  0.1625

__Solution.__ This one has to do with the [law of total probability](http://en.wikipedia.org/wiki/Law_of_total_probability). Applying the law, we have
`\[
P(A) = P(A|B_1) \cdot P(B_1) + P(A|B_2) \cdot P(B_2) = \frac{1}{5} \cdot \frac{3}{4} + \frac{1}{20} \cdot \frac{1}{4} = \frac{13}{80} = 0.1625,
\]`
where `\( P(A) \)` is what we are looking for; `\( P(B_1) = \frac{3}{4} \)` is the probability that a passing train is a passenger train; `\( P(A|B_1) = \frac{1}{5} \; (20\%) \)` is the probability that a passenger train stops at Blue Oaks; `\( P(B_2) = 1-\frac{3}{4} = \frac{1}{4} \)` is the probability that a passing train is a freight train; `\( P(A|B_2) = \frac{1}{20} \; (5\%) \)` is is the probability that a freight train stops at Blue Oaks.

Thus, there's a 16,25% chance that a passing train stops at the station.
