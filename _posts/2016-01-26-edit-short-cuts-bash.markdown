---
layout: post
title:  Edit shortcuts in bash
comments: true
date:   2016-01-26
---

1. Open the *.bash_profile* file with your favorite editor (for instance C-x C-f in emacs and search for the file: ~/.bash_profile)


2. Write your aliases in the *.bash_profile* like:

* alias vw1='vw click_train.vw -c -k --passes 10 --loss_function=logistic --link=logistic -f click_model.vw'
* alias vw2='vw click_test.vw -t -i click_model.vw -p click_predictions.txt'
* alias score='python score_vw.py click_test.vw click_predictions.txt '
* alias nb='ipython notebook'
* alias py3='source activate python3'

The first three aliases are for vowpal wabbit routines I've been using a lot. 

The fourth one is really useful to launch Ipython Notebook. 

The last one is to switch to python 3. Before that I had to create a 'conda' environment for python 3 with

> conda create -n python3 python=3.4

3. Force the .bash_profile to execute. This loads the values immediately without having to reboot. In your Terminal window, run the following command.

> $ source ~/.bash_profile

4. Then, enjoy your shortcuts in Terminal! Launch a notebook in python 3 with just 4 letters and 1 number!

> $ macbook-pro-de-lecue:~ lecueguillaume$ py3
> 
> discarding /Users/lecueguillaume/anaconda/bin from PATH
> 
> prepending /Users/lecueguillaume/anaconda/envs/python3/bin to PATH
> 
> $ (python3)macbook-pro-de-lecue:~ lecueguillaume$ nb
