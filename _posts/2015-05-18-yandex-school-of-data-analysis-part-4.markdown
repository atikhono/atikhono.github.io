---
layout: post
title:  "Yandex School of Data Analysis Part 4. Programming"
date:   2015-05-18 21:02:54
external: [latex]
---

This is part 4. I'm using Python2.
There are also some general requirements for both algorithms:

* Time limit 1 second
* Memory limit 64Mb
* Input: stdin or file input.txt
* Output: stdout or file output.txt
<!--more-->

####__J. Palindrome__

Check if a string is a palindrome. Return `yes` if true, `no` otherwise.

The string contains no spaces. The maximum string length is 200. Lowercase and uppercase letters are considered different.

Example:

* Input: `abba`
  
  Output: `yes`
* Input: `qwerq`
  
  Output: `no`

__Solution.__
Function `pal(s)` checks if string `s` is a palindrome.

{% highlight python %}
def pal(s):
    for i,char in enumerate(s):
        if s[-i-1] != char:
            return "no"
    return "yes"
{% endhighlight %}


####__I. Shoe store__

A customer visits a shoe store. How many pairs of shoes can he put on at the same time? Shoes can be worn over other shoes if they are at least 3 sizes bigger.

The first input line contains the size the customer usually wears. The second line contains the total number of shoe pairs in the store. The third line contains the shoe sizes available in the store. Sizes are natural numbers that are less of equal 100. The total number of shoe pairs in the store is less or equal 1000.

Example:

* Input:
{% highlight python %}
60
2
60 63
{% endhighlight %}

  Output: `2`

* Input:
{% highlight python %}
26
5
30 42 40 41 35
{% endhighlight %}

  Output: `3`

__Solution.__
Function `store(l,size)` computes the number of shoe pairs the customer can put on at the same time. List `l` contains the sizes available in the store. Integer `size` is the size the customer wears.
{% highlight python %}
def store(l,size):
    n = 0
    for i in sorted(set(l)):
        if i == size or i >= size + 3:
            n = n + 1
            size = i
    return n
{% endhighlight %}

`sorted(set(l))` eliminates duplicates and sorts the list.
