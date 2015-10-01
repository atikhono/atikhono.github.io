---
layout: post
title:  "Split git repositories"
date:   2015-09-15 17:20:01
categories: git
external: [noexcerpt]
---

Recently I've had my thesis published in [UH Research Archive](http://hdl.handle.net/2299/16341) and I think I should publish my code to complement it. We have a private repository for the whole project on Bitbucket and my project is a small part of what should not get public yet. So in order to publish, I should strip my code out of the big one. And anyway, someone will have to do it someday as the project grows. Below I will shed some light on how to turn a directory within a git repository into a brand new repository.

First of all, clone the repository that contains the directory you want to move:
{% highlight bash %}
git clone REPO
{% endhighlight %}

Then run `git filter-branch` with the name of this directory:
{% highlight bash %}
## Filter the master branch to your directory and remove empty commits
git filter-branch --prune-empty --subdirectory-filter DIR master
{% endhighlight %}

The clone now contains all the files that were in your (sub-)directory. Note that although all of your previous files have been removed, they still exist within the git history. The `--prune-empty` switch allows to ignore empty commits that the filter might generate.

An alternative way to go would be to filter the subdirectory into a new branch of the existing repository:
{% highlight bash %}
cd REPO
git subtree split -P DIR -b NEW_DIR_BRANCH
{% endhighlight %}

Then you might want to initialize a new git repository and pull the branch in there:
{% highlight bash %}
git pull REPO NEW_DIR_BRANCH
{% endhighlight %}

Now, you might want to remove some unneeded files from the history if any:
{% highlight bash %}
git filter-branch --index-filter \
    'git rm --cached --ignore-unmatch -f FILE_TO_REMOVE' -f --prune-empty HEAD
{% endhighlight %}

That's it. If you need to modify the history including the root commit, rebase with the `--root` switch
{% highlight bash %}
git rebase -i --root master
{% endhighlight %}

My project on github: [Astrakahn synchroniser compiler](https://github.com/atikhono/astrakahn-sync).
