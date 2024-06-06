---
layout: post
title:  Installation de CVXPY sous windows.
comments: true
date:   2017-03-14
---

a) On suppose que Anaconda et CVXOPT sont installés

b) Aller sur [librairies python pour windows](http://www.lfd.uci.edu/~gohlke/pythonlibs/)

c) Télécharger :

1) [ecos pour win64 et python 3.5](http://www.lfd.uci.edu/~gohlke/pythonlibs/#ecos) télécharger 
    * ecos‑2.0.4‑cp35‑cp35m‑win_amd64.whl *

2) [SCS](http://www.lfd.uci.edu/~gohlke/pythonlibs/#ecos) télécharger 
    * scs‑1.2.6‑cp35‑cp35m‑win_amd64.whl *

3) [cvxpy pour win64 et python 3.5](http://www.lfd.uci.edu/~gohlke/pythonlibs/#ecos)
    * cvxpy‑0.4.9‑py3‑none‑any.whl * 


d) ouvrir un éditeur de commandes en mode admin

e) taper 

    pip install "chemin du fichier ecos"

f) taper 

    pip install "chemin du fichier SCS"

g) taper 

    pip install "chemin du fichier cvxpy"

f) tester en tapant "python" puis <Enter> dans le terminal et en exécutant la ligne de code suivante: "import cvxpy". Si l'installation est réussie, le prompt revient sans erreur.




 