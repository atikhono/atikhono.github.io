---
layout: post
title:  "Yandex School of Data Analysis 2015"
date:   2015-05-15 14:56:34
external: [latex]
---

For the first time I've heard about the [Yandex School of Data Analysis](http://yandexdataschool.com/about) in the beginning of my undergraduate studies at MEPhI. Actually, the School was founded in 2007, the year I started at MEPhI, and later I felt like it gained good reputation among highly-motivated students in no time. The School kind of targeted future [Yandex](http://yandex.ru) employees, but I had no intention to work at Yandex at that time so I never even thought of applying there. However, from time to time I saw some of my brightest fellow classmates struggle with some entrance tests from the School.

Recently a friend reminded me that the application for the year 2015 has been open, and he got me to apply. The application deadline was in two weeks or so, but I was mostly interested in the tests they offer than in preparing the actual application.

The admission to the School happens in three stages. Firstly, stage applicants fill out a registration form and provide information on their background and motivation to enter the School. After having filled the form, applicants are offered ten little problems to sanity-check their abilities in basic math and programming. Secondly, depending on the sanity test results, the School invites successful applicants to take a written exam at a Yandex office (or another location provided by the School). Thirdly, those who were selected by the results of the exam have an interview with the professors of the School. Lastly, those who succeeded in the interview are invited to join the School.

At some point before it was too late, I found out that the School offers [a brilliant program](http://yandexdataschool.com/edu-process) at the Data Analysis department and submitted the answers to my sanity test. I would like to share the problems from the test because as far as I know they are not published officially. For each problem I give the answer I submitted and explain how I got it.

I don't like long posts so I divided the test into four parts: calculus, linear algebra, combinatorics and probability, and programming. This is part 1 -- calculus. I'm using [Maxima](http://maxima.sourceforge.net) 5.34.1 to check myself.

<!--more-->

####__A. Limit of a sequence__
Find

$$
\lim_{n \rightarrow \infty} (\frac{1}{n^2} + \frac{2}{n^2} + \frac{3}{n^2} + \dots + \frac{n-1}{n^2})
$$

__Answer.__  $\frac{1}{2}$

__Solution.__  First of all, we can rewrite the given sequence as $\frac{1+2+3+ \dots + (n-1)}{n^2}$. The summands $1, 2, 3, \dots, (n-1)$ of the sequence nominator form a finite <a href="http://en.wikipedia.org/wiki/Arithmetic_progression">arithmetic progression</a> of $(n-1)$ members with the initial term $a_1 = 1$ and common difference of successive members $d = 1$, thus,

$$
1+2+3+ \dots +(n-1) = (n-1) \cdot \frac{(a_1 + (n-1))}{2} = (n-1) \cdot \frac{(1 + (n-1))}{2} = \frac{(n-1)n}{2}
$$

Then,

$$
\lim_{n \rightarrow \infty} \frac{1+2+3+ \dots + (n-1)}{n^2} = \lim_{n \rightarrow \infty} \frac{(n-1)n}{2n^2} = \lim_{n \rightarrow \infty} \frac{n-1}{2n} = \frac{1}{2}
$$


####__B. Limit of a function__
Find

$$
\lim_{x \rightarrow -8} \frac{\sqrt{1-x} - 3}{2 + \sqrt[3]{x}}
$$

__Answer.__  $-2$

__Solution__.  We shall note that both $f(x) = \sqrt{1-x} - 3$ and $g(x) = 2 + \sqrt[3]{x}$ turn $0$ in $x=-8$, thus, $\frac{f(-8)}{g(-8)}$ is the indeterminate form $\frac{0}{0}$. Functions $f(x)$ and $g(x)$ are differentiable on an open interval $|x + 8| < \varepsilon$:

$$
\begin{align}
f'(x) &= \frac{d}{dx}(\sqrt{1-x} - 3) = -\frac{1}{2\sqrt{1-x}}\\
g'(x) &= \frac{d}{dx}(2 + \sqrt[3]{x}) = \frac{1}{3\sqrt[3]{x^2}}
\end{align}
$$

Now we can see that $g'(x) \ne 0$ on $|x + 8| < \varepsilon$, and the <a href="http://en.wikipedia.org/wiki/L%27Hôpital%27s_rule">L'Hôpital's rule</a> can be applied:

$$
\lim_{x \rightarrow -8}\frac{f(x)}{g(x)} = \lim_{x \rightarrow -8}\frac{f'(x)}{g'(x)} = \lim_{x \rightarrow -8}\frac{-3\sqrt[3]{x^2}}{2\sqrt{1-x}} = \frac{-3\sqrt[3]{64}}{6} = -2
$$

Maxima code:
{% highlight ruby %}
limit(((1-x)^(1/2)-3)/(2+x^(1/3)), x, -8);
#=> -2
{% endhighlight %}


####__C. Integral__
Find

$$
\int_{0}^{1}x^2 e^{3x} dx
$$

Round the result to nearest 6 decimal places.

__Answer.__  3.64547

__Solution.__  Integrals $\int x^n e^x dx$ can be evaluated repeatedly using <a href="https://en.wikipedia.org/wiki/Integration_by_parts">integration by parts</a>; each application of the method lowers the power of $x$ by 1. Integration by parts states that for two continuously differentiable functions $u$ and $v$ $\int u \: dv = uv - \int v \: du$.

$$
\begin{align}
\int_{0}^{1}x^2 e^{3x} dx &= \int_{0}^{1}x^2 d(\frac{e^{3x}}{3})\\
&= \frac{1}{3} \lgroup x^2 e^{3x} \bracevert_{0}^{1} - \int_{0}^{1}2x \: e^{3x} dx \rgroup\\
&= \frac{1}{3} \lgroup e^3 - \int_{0}^{1} 2x \: d(\frac{e^{3x}}{3}) \rgroup\\
&= \frac{1}{3} \lgroup e^3 - \frac{2}{3} \lgroup x \: e^{3x} \bracevert_{0}^{1} - \int_0^1 e^{3x}dx \rgroup \rgroup\\
&= \frac{1}{3} \lgroup e^3 - \frac{2}{3} \lgroup e^3 - \frac{1}{3} e^{3x} \bracevert_0^1 \rgroup \rgroup\\
&= \frac{5}{27} e^3 - \frac{2}{9} = 3.6454698005\dots\\
\end{align}
$$

The rounding is obvious.

Maxima code:
{% highlight ruby %}
float(integrate(x^2 * %e^(3*x), x, 0, 1));
#=> 3.645469800590309
{% endhighlight %}
