---
layout: post
title:  "Yandex Test Results"
date:   2015-05-19 22:20:49
external: [latex,noexcerpt]
---

I have just got a mail from the admission team. I am invited to take part in the entrance exam, but I made a mistake in problem __E__ and I want to correct myself. Let me remind what problem __E__ was.

Find all `\( a \)` values for which the matrix below has rank 2 `\[
\left(\begin{array}{ccc}
a-1 & a-1 & a(a-1)\\
2a-3 & 3a-5 & a^2-2\\
-1 & a-3 & 4a-5\\
\end{array}\right)
\]`

The rank of a matrix is the number of linearly independent columns or rows. The answer I gave was `\( a=1 \)` and `\( a=2 \)`. When `\( a=1 \)` the given matrix turns `\(
\begin{bmatrix}
0 & 0 & 0\\
-1 & -2 & -1\\
-1 & -2 & -1\\
\end{bmatrix} \)`.

But the rank of that matrix equals 1 as all its rows are linearly dependent. Oops :)
