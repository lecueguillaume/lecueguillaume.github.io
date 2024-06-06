---
layout: post
title:  Restore variables after notebook crashed
comments: true
date:   2017-06-19
---

#Recover variables after a cell in a python notebook fails
After python lost connexion with my browser (here safari) while using Jupyter notebook

    WebSocket ping timeout after 91539 ms

I wanted to recover some variables like a dictionary. I should have use the **try: except:** protocole but I did not so I end up with a notebook not working and variables that I was not able to get back. Here is a solution that worked for me:

1) I interrupted the kernel

    Kernel interrupted: d3d55f0d-52f1-4660-a43b-1fedb698452f

(I got the address of the kernel. Note that it is different from the Kernel address when it started: f757186e-0570-467a-918e-934bb48dee45)

2) I went to the terminal and typed:

    $ ipython console --existing d3d55f0d-52f1-4660-a43b-1fedb698452f.json

This opened an ipython consol (you can replace *ipython* with *jupyter*)

3) I listed all the local variables to check that my *dictionary* was in there:

    locals()

I was pretty happy to see my variable *dict_final* in the list.

4) then I *pickle.dump* my dictionary in the consol:

    import pickle
    filename = 'dict_final.p'
    with open(filename, "wb") as f:
        pickle.dump(dict_final, f)

5) Once my variable has been pickled down, I can load it in any other notebook where I want to use it via (in a notebook):

    import pickle
    filename = 'dict_final.p'
    with open(filename, "r") as f:
        pickle.load(dict_final, f)






 