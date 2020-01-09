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

Now what you can do is make another `.rst` file that contains a template for methods and another for classes (have a look around in the contents of `pysseract` for this). That way, you can have all the bits you need auto-formatted and in a separate page as needed. There's also a fiddle needed to make sure that tables don't run off the page, which is achieved by means of a CSS file (this can be found in the `docs` subdirectory of `pysseract` as well).

From this point on, if you can build documentation locally with all this set up it will just be a matter of adding docstrings every time you add a new method or class.

# Step 2: build

This bit was extremely fiddly. The main reason for this is actually pretty simple. To ensure that your package can work on as many different linux distributions as possible, you need to build it on a really old one. This is where the `manylinux` standard comes in. Long story short, someone decided that it would be sane to make a Docker image that has a really old version of CentOS (a Red Hat derivative), in it that package maintainers can use for building. It turns out this has been updated a few times and there are now a couple of types of `manylinux` corresponding to the following:

- `manylinux1`      -> CentOS 5
- `manylinux2010`   -> CentOS 6
- `manylinux2014`   -> CentOS 7

CentOS 5 is end-of-life at this point, so you should only really need to use it if you're trying to be really exhaustive about compatibility for maintaining compiled code. If you aren't actually compiling anything, then this isn't really an issue.

Either way, that's more or less what the build process looks like. Clone one of the `manylinux` docker images, then perform your build process inside it. To do this within a build framework like Travis CI or similar, what you'll do is something like this:

- Get a copy of the Docker image you're interested in and mount it
- Run a script on the image that will:
    - Perform the build
    - Run tests as appropriate
    - Use `auditwheel` (part of `setuptools`) or similar to ensure that external dependencies (e.g. compiled code) are contained within the wheel you build
    - Send the wheels off to test PyPI to check that all's well with that part of the process
- Get the wheel objects from the mounted image and send them off to real PyPI

This might sound a little involved but isn't as much of a pain as it seems.

# Something else: versioning

Another thing you'll want to think about is making sure the version numbers are accurate for your package. This is pretty easily achieved with [Git Flow](https://github.com/petervanderdoes/gitflow-avh). All you need to do is use the macros to create a release every time you want to update `Master` and then just tag the final commit with the version number before you merge the branch. The tag can be detected as an environment variable by Travis and used as part of the build process. So then when you put it all together, every time you want to update the package you will just do the following:

- Write the code
- Write the docstrings and tests
- Open a release branch and commit it all
- Finalise the branch, then commit and push

Then you'll get the building, testing, documentation and versioning done automatically. Easy!