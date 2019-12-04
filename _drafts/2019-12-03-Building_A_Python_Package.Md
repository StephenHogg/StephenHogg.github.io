---
layout: post
title: "Building A Python Package: How Hard Is It?"
---

[Hong](https://xiahongze.github.io) and I recently published our first python package together. It's called [Pysseract](https://pypi.org/project/pysseract/) and is now available through PyPI. We thought about Conda, but aren't going to bother for now unless someone tells us we should.

Making the code that we packaged was simple enough; turning it into a package was noticeably more difficult. So, partly for therapeutic reasons and partly for your benefit, I'll use this post to talk through some of the things we found out in the process.

# What needs doing

In our case, we wanted to achieve the following:

- Get Travis CI to handle the building, testing and pushing to PyPI;
- Get everything well-documented, and then;
- Get the documentation built and published automatically

With all of these things together, pushing new versions would be very simple. Just open a branch, and when you're ready merge it to master. 

Throughout all of this, however, things were just a little more difficult than they seemed for one reason. Code compilation.

# Step 1: documentation

The first part is fairly straightforward. What you do is put docstrings on all your functions and classes, so that they can be picked up when documentation is generated.

After that it gets more complicated. You need to register an account at [readthedocs.org](https://readthedocs.org/), which shouldn't be too hard because it integrates with a GitHub account if you've got one. Then, you need to set up a webhook in your GitHub repo so that every time you update master, for instance, readthedocs will get told to start a build. A bit of Googling makes this fairly easy. If you don't want this to be automated then you can always just trigger the readthedocs build on their website manually.

Now the question of the actual build job. There are a few bits and pieces to make this easier, most notably the python package [`sphinx_rtd_theme`](https://pypi.org/project/sphinx-rtd-theme/). This thing works with [`sphinx`](http://www.sphinx-doc.org/en/master/), a python document generator, to create documentation in the format readthedocs expects. 

So far so good. How to tell sphinx what should or shouldn't be in your documentation? What you need are a couple of files and a directory structure. First of all you'll need an `index.rst` - this will contain the landing page of your documentation, more or less. One thing we did to try and make this more interesting was get it to include the contents of our `README.MD` file using another package called `m2r`.