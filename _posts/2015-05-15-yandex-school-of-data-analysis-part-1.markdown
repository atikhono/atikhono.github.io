---
layout: post
title:  "Yandex School of Data Analysis Part 1. Calculus"
date:   2015-05-15 14:56:34
external: [latex]
---

This is part 1.
I'm using <a href="http://maxima.sourceforge.net">Maxima</a> 5.34.1 and Python2 to check myself.

####__A. Limit of a sequence__
Find
`\[
\lim_{n \rightarrow \infty} (\frac{1}{n^2} + \frac{2}{n^2} + \frac{3}{n^2} + \dots + \frac{n-1}{n^2})
\]`

__Answer.__  `\( \frac{1}{2} \)`

__Solution.__  First of all, we can rewrite the given sequence as `\( \frac{1+2+3+ \dots + (n-1)}{n^2} \)`. The summands `\( 1, 2, 3, \dots, (n-1) \)` of the sequence nominator form a finite <a href="http://en.wikipedia.org/wiki/Arithmetic_progression">arithmetic progression</a> of `\( (n-1) \)` members with the initial term `\( a_1 = 1 \)` and common difference of successive members `\( d = 1 \)`, thus,
`\[
1+2+3+ \dots +(n-1) = (n-1) \cdot \frac{(a_1 + (n-1))}{2} = (n-1) \cdot \frac{(1 + (n-1))}{2} = \frac{(n-1)n}{2}
\]`
Then,
`\[
\lim_{n \rightarrow \infty} \frac{1+2+3+ \dots + (n-1)}{n^2} = \lim_{n \rightarrow \infty} \frac{(n-1)n}{2n^2} = \lim_{n \rightarrow \infty} \frac{n-1}{2n} = \frac{1}{2}
\]`


####__B. Limit of a function__
Find
`\[
\lim_{x \rightarrow -8} \frac{\sqrt{1-x} - 3}{2 + \sqrt[3]{x}}
\]`

__Answer.__  `\( -2 \)`

__Solution__.  We shall note that both `\( f(x) = \sqrt{1-x} - 3 \)` and `\( g(x) = 2 + \sqrt[3]{x} \)` turn `\( 0 \)` in `\( x=-8 \)`, thus, `\( \frac{f(-8)}{g(-8)} \)` is the indeterminate form `\( \frac{0}{0} \)`. Functions `\( f(x) \)` and `\( g(x) \)` are differentiable on an open interval `\( |x + 8| < \varepsilon \)`:
`\[
\begin{align}
f'(x) &= \frac{d}{dx}(\sqrt{1-x} - 3) = -\frac{1}{2\sqrt{1-x}}\\
g'(x) &= \frac{d}{dx}(2 + \sqrt[3]{x}) = \frac{1}{3\sqrt[3]{x^2}}
\end{align}
\]`

Now we can see that `\( g'(x) \ne 0 \)` on `\( |x + 8| < \varepsilon \)`, and the <a href="http://en.wikipedia.org/wiki/L%27Hôpital%27s_rule">L'Hôpital's rule</a> can be applied:
`\[
\lim_{x \rightarrow -8}\frac{f(x)}{g(x)} = \lim_{x \rightarrow -8}\frac{f'(x)}{g'(x)} = \lim_{x \rightarrow -8}\frac{-3\sqrt[3]{x^2}}{2\sqrt{1-x}} = \frac{-3\sqrt[3]{64}}{6} = -2
\]`

Maxima code:
{% highlight ruby %}
limit(((1-x)^(1/2)-3)/(2+x^(1/3)), x, -8);
#=> -2
{% endhighlight %}


####__C. Integral__
Find
`\[
\int_{0}^{1}x^2 e^{3x} dx
\]`
Round the result to nearest 6 decimal places.

__Answer.__  3.64547

__Solution.__  Integrals `\( \int x^n e^x dx \)` can be evaluated repeatedly using <a href="https://en.wikipedia.org/wiki/Integration_by_parts">integration by parts</a>; each application of the method lowers the power of `\( x \)` by 1. Integration by parts states that for two continuously differentiable functions `\(u\)` and `\(v\)` `\( \int u \: dv = uv - \int v \: du \)`.
`\[
\begin{align}
\int_{0}^{1}x^2 e^{3x} dx &= \int_{0}^{1}x^2 d(\frac{e^{3x}}{3})\\
&= \frac{1}{3} \lgroup x^2 e^{3x} \bracevert_{0}^{1} - \int_{0}^{1}2x \: e^{3x} dx \rgroup\\
&= \frac{1}{3} \lgroup e^3 - \int_{0}^{1} 2x \: d(\frac{e^{3x}}{3}) \rgroup\\
&= \frac{1}{3} \lgroup e^3 - \frac{2}{3} \lgroup x \: e^{3x} \bracevert_{0}^{1} - \int_0^1 e^{3x}dx \rgroup \rgroup\\
&= \frac{1}{3} \lgroup e^3 - \frac{2}{3} \lgroup e^3 - \frac{1}{3} e^{3x} \bracevert_0^1 \rgroup \rgroup\\
&= \frac{5}{27} e^3 - \frac{2}{9} = 3.6454698005\dots\\
\end{align}
\]`
The rounding is obvious.

Maxima code:
{% highlight ruby %}
float(integrate(x^2 * %e^(3*x), x, 0, 1));
#=> 3.645469800590309
{% endhighlight %}
