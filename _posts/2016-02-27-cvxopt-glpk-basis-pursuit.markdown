---
layout: post
title:  Install glpk with CVXOPT on python
comments: true
date:   2016-02-27
---
Here are some explaination on how to install glpk and CVXOPT (on MAC). Using option 'glpk' in solvers.lp method of CVXOPT speeds up cvxopt by a factor of 2 or 10  according to  [Stephane Caron's webpage](https://scaron.info/blog/linear-programming-in-python-with-cvxopt.html) 


a) Install glpk via brew :

> brew install glpk

b) The GLPK interface is not enabled by default. You need to edit the setup.py of CVXOPT. In my case, I have this file in the following folder

> Google\ Drive/package_python/cvxopt-1.1.7/setup.py

 First thing, set variable BUILD_GLPK to 1: 

>BUILD_GLPK = 1 

Then indicate the path to *libglpk*

>GLPK_LIB_DIR = '/usr/local/Cellar/glpk/4.52/lib'

Then indicate the path to *glpk.h*

>GLPK_INC_DIR = '/usr/local/Cellar/glpk/4.52/include'

c) Go to the CVXOPT's 'setup.py' folder and run

> python setup.py install

d) Enjoy CVXOPT with glpk :

> sol = solvers.lp(c, G, h, A, b, solver = 'glpk')
