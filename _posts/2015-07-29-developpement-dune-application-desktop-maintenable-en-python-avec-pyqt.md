---
ID: 83
post_title: 'Développement d&rsquo;une application desktop maintenable en Python avec PyQt'
author: Titouan BENOIT
post_date: 2015-07-29 14:11:55
post_excerpt: ""
layout: post
permalink: >
  http://blog.nbcorp.fr/2015/07/developpement-dune-application-desktop-maintenable-en-python-avec-pyqt/
published: true
post_views_count:
  - "745"
---
Bonjour à tous,

aujourd'hui je vais faire un petit tutoriel sur comment faire une application desktop en Python avec PyQt. Pour ceux qui ne connaissent pas <a href="http://www.qt.io/">Qt</a>, c'est une librairie graphique qui fournit pas mal d'outils sympas pour faire des interfaces graphiques. Vraiment puissant et sympa à utiliser, je le conseille vivement pour des projets de toutes tailles qui ont besoin d'avoir un client desktop.

<!--more-->

Une question légitime est "Pourquoi choisir de faire une application desktop en <a href="https://www.python.org/">Python</a> ??". En effet, c'est une bonne question. Dans un premier temps je dirais que le Python est multiplateforme et donc votre application fonctionnera sur Windows, Mac OS X et Linux ayant Python. De plus, personnellement je fais des applications desktop en Python principalement pour venir communiquer en Serial avec des systèmes embarqués (Communication Serial avec une Arduino, MBED ou un micro STM32). Ces applications me permettent d'avoir une interface graphique sympa pour venir configurer une Arduino par exemple. Le langage est vraiment facile à utiliser et performant, et couplé avec <a href="https://pip.pypa.io/en/stable/">pip</a> le gestionnaire de dépendances on fait des projets vraiment propres en un temps record ;).

Maintenant que j'ai introduit le sujet, je vous propose de mettre en place une application très simple avec Python et PyQt ainsi qu'un environnement facile à maintenir.
<h2>1. Prérequis</h2>
Pour ceux qui développent sous Linux :
<ul>
	<li>Python 2.7.x</li>
	<li>PyQt4 : <code>sudo apt-get install pyqt4-dev</code></li>
	<li>PyQt4 Tools : <code>sudo apt-get install pyqt4-dev-tools</code></li>
	<li>Qt-designer : <code>sudo apt-get install qt4-designer</code></li>
</ul>
<span style="font-family: arial,helvetica,sans-serif;">Pour ceux sous Windows : </span>
<ul>
	<li>Python 2.7.x</li>
	<li>PyQt4 : <a href="http://www.riverbankcomputing.co.uk/software/pyqt/download">http://www.riverbankcomputing.co.uk/software/pyqt/download</a></li>
</ul>
Pour ma part, je travaille sous Linux Mint 17.10 et pour coder le super éditeur Sublime Text 3.
<h2>2. Qt Designer</h2>
Qt Designer est l'outil qui vous permet de construire vos interfaces graphiques aussi appelé GUI (Graphical User Interface) ou simplement UI (User Interface).

<a href="http://blog.nbcorp.fr/wp-content/uploads/2015/07/QtDesigner.png"><img class="alignnone size-large wp-image-89" src="http://blog.nbcorp.fr/wp-content/uploads/2015/07/QtDesigner-1024x496.png" alt="QtDesigner" width="730" height="354" /></a>

A partir de cet outil, vous êtes capable de créer très facilement et rapidement vos interfaces graphique. Du simple drag&amp;drop et le tour est joué ! Ensuite, Qt designer enregistre l'UI au format .ui qui est simplement un format xml spécifique à Qt.

Une fois notre interface réalisée, on peut à partir du fichier .ui réaliser une classe Python pour PyQt. On réalise ceci grâce à <strong>pyuic4.</strong>
<pre class="lang:default decode:true">pyuic4 monfichier.ui -o monfichier.py</pre>
Et on récupère une classe Python qui correspond à notre UI et qu'on va pouvoir manipuler en Python. Il faut à présent faire un petit scaffolding pour notre projet afin de faciliter l'intégration de l'UI dans notre app.
<h2>3. Scaffolding</h2>
Je propose un scaffolding comme ceci : (note : en <strong>gras</strong> les dossiers en <em>italique</em> les fichiers)
<ul>
	<li><strong>project</strong>
<ul>
	<li><em>appName.py</em></li>
	<li><em>App.py</em></li>
	<li><em>MainUI.py</em></li>
	<li><em>__init__.py</em></li>
	<li><strong>UI</strong>
<ul>
	<li><em>myui.ui</em></li>
	<li><em>MyUI.py</em></li>
	<li><em>build.sh</em></li>
</ul>
</li>
</ul>
</li>
</ul>
<a href="http://blog.nbcorp.fr/wp-content/uploads/2015/07/scaffolding.png"><img class="alignnone size-full wp-image-99" src="http://blog.nbcorp.fr/wp-content/uploads/2015/07/scaffolding.png" alt="scaffolding" width="211" height="218" /></a>

Pour expliquer le principe, tous ce qui est lié à mon UI est dans le dossier<strong> UI</strong> (*.ui, mes classes Python générées à partir des *.ui, ressources tel que Images, ...). Mon script <em>build.sh</em> me permet de convertir mon fichier <em>myui.ui</em> en <em>MyUI.py</em>.

<em>build.sh</em>
<pre class="lang:default decode:true" title="build.sh">#!/bin/bash

pyuic4 myui.ui -o MyUI.py
#pyrcc4 ressources.qrc -o Ressources_rc.py</pre>
La magie s'opère ensuite dans le fichier MainUI.py ; en effet, je vais créer une classe MainUI qui va hériter de la classe MyUI du fichier MyUI.py

Grâce à ce système, si je fais des modifications sur mon UI via Qt designer, je n'ai qu'à exécuter mon script build.sh pour mettre à jour mon UI.
<h2>4. Organisation du code</h2>
Le fichier MainUI.py hérite de notre MyUI.py généré depuis le fichier de Qt Designer :
<pre class="lang:python decode:true">#!/usr/bin/python
# -*- coding: UTF-8 -*-
#***************************************************************************#
#                                                                           #
#                              MainUI.py                                    #
#                                                                           #
#***************************************************************************#
#                                                                           #
# Class MainUI extend from Ui_MainWindow which is generated with #
# py2uic and QtDesigner.                                                    #
#                                                                           #
#                                                                           #
#***************************************************************************#
# Création     : 29.07.2015  T. Benoit       Version 1.0                    #
# Vérifié      : @@.@@.@@@@  T. Benoit                                      #
# Modification :                                                            #
#***************************************************************************#

import sys
import UI.MyUI as MyUI
from PyQt4 import QtCore, QtGui

try:
    _fromUtf8 = QtCore.QString.fromUtf8
except AttributeError:
    def _fromUtf8(s):
        return s


class MainUI(QtGui.QMainWindow, MyUI.Ui_MainWindow):
    def __init__(self, parent=None):
        super(MainUI, self).__init__(parent)
        self.setupUi(self)

        # customize UI here

 
    def main(self):
        self.show()
</pre>
On peut ici personnaliser notre UI avec des comportements particuliers comme lier un bouton pour ouvrir une boite de dialogue, ... On met ici des fonctionnalités liées à l'UI mais pas encore des fonctionnalités liées à l'application en elle même. Les fonctionnalités liées à l'application vont se trouver dans le fichier App.py !

App.py
<pre class="lang:python decode:true">#!/usr/bin/python
# -*- coding: UTF-8 -*-
#***************************************************************************#
#                                                                           #
#                                 App.py                                    #
#                                                                           #
#***************************************************************************#
#                                                                           #
# Class App which contains application logic                                #
#                                                                           #
#                                                                           #
#                                                                           #
#***************************************************************************#
# Création     : 29.07.2015  T. Benoit       Version 1.0                    #
# Vérifié      : @@.@@.@@@@  T. Benoit                                      #
# Modification :                                                            #
#***************************************************************************#


from MainUI import MainUI
from PyQt4 import QtCore, QtGui



#---------------------------------------------------------------------------#

try:
    _fromUtf8 = QtCore.QString.fromUtf8
except AttributeError:
    def _fromUtf8(s):
        return s

#---------------------------------------------------------------------------#

class App:

    gui = None
    app = None
    counter = 0

    def __init__(self, guiClass, appClass):
        self.gui = guiClass
        self.app = appClass
        self.counter = 0

    def setup(self):
        """ setup functionnality """
        
        self.gui.pushButton.clicked.connect(self.action)


    def main(self):
        """ Main execution for App """
        self.setup()
        self.gui.main()


    def action(self):
        """ action when I click the push Button """
        self.gui.textEdit.append("Hello world: "+str(self.counter))
        self.counter = self.counter + 1</pre>
On retrouve ici la base de notre application, on injecte la classe avec l'ui afin de pouvoir manipuler les objets de l'interface graphique. La méthode setup permet d'initialiser les connect qui sont des listeners d’événement pour PyQt. On y attache des fonctions callbacks qui seront exécutés si l'événement survient. Par exemple ici j'ai attaché l'événement clicked sur le bouton pushButton à la méthode action de la classe. Dans cette méthode, je remplis le textEdit avec hello world et un compteur.

La class App est le coeur de votre application, c'est là où vous mettez la logique de votre app.

Enfin, il faut le fichier de l'application qui sera à exécuter :

appName.py
<pre class="lang:python decode:true">#!/usr/bin/python
# -*- coding: UTF-8 -*-
#***************************************************************************#
#                                                                           #
#                              appName.py                                   #
#                                                                           #
#***************************************************************************#
#                                                                           #
# Main file for our Application                                             #
#                                                                           #
#                                                                           #
#                                                                           #
#***************************************************************************#
# Création     : 29.07.2015  T. Benoit       Version 1.0                    #
# Vérifié      : @@.@@.@@@@  T. Benoit                                      #
# Modification :                                                            #
#***************************************************************************#

import sys
from MainUI import MainUI
from App import App
from PyQt4 import QtCore, QtGui

def main():
    app = QtGui.QApplication(sys.argv) #create a Qt app
    gui = MainUI() # create GUI instance
    myApp = App(gui,app)
    myApp.main() # init the App
    sys.exit(app.exec_()) # lauch Qt App

#---------------------------------------------------------------------------#
#                                Main                                       #
#---------------------------------------------------------------------------#

if __name__=='__main__':
    main()</pre>
Dans un premier temps, on créé une Qt app puis on instancie notre GUI qui vient du MainUI et enfin on instancie notre classe App en lui injectant le gui et l'app Qt pour qu'elle puisse les manipuler. Le must serait d'instancier la classe MainUI dans un thread et l'App dans un autre thread car si vous avez des fonctions dans la classe App qui prennent du temps ou qui sont bloquantes, cela va freezer l'interface graphique... pas cool... Mais dans la majorité des cas, on clique sur un bouton et on fait une action simple non bloquante dans ce cas là pas besoin de séparer l'App et l'UI dans deux threads différents.

Et voilà, vous n'avez plus qu'à exécuter votre application : python appName.py
<h2> 5. Pour aller plus loin...</h2>
Maintenant qu'on a notre application, on voudrait bien en faire un .exe sous Windows afin de livrer une app packagée. Pour cela, il existe l'utilitaire <a href="http://www.py2exe.org/">py2exe</a> qui est franchement bien !

Il faut juste créer un fichier setup.py à la racine de notre projet avec la configuration de notre application :

setup.py
<pre class="lang:python decode:true ">from distutils.core import setup
import sys
import py2exe

setup(name="appName",
      version="1.0.0",
      author="Titouan Benoit",
      author_email="titouan.benoit@gmx.fr",
      windows=[{"script": "appName.py"}],
      options={"py2exe": {'bundle_files': 1, 'compressed': True,"includes": ["sip"], "dll_excludes": ["MSVCP90.dll", "HID.DLL", "w9xpopen.exe"]}})</pre>
Et ensuite exécuter :
<pre class="code highlight white plaintext"><code>python setup.py py2exe</code></pre>
Attention, cela fonctionne uniquement sous Windows bien entendu et il vous faut Microsoft Visual C++ 2008 : <a href="http://www.microsoft.com/fr-FR/download/details.aspx?id=29">download</a>

Vous avez ensuite un appName.exe et un library.zip que vous pouvez distribuer !
<h2>6. Références et code source</h2>
Voici les deux endroits où vous pourrez trouver des informations pour PyQt :
<ul>
	<li><a href="http://pyqt.sourceforge.net/Docs/PyQt4/index.html">http://pyqt.sourceforge.net/Docs/PyQt4/index.html</a></li>
	<li><a href="http://pyqt.sourceforge.net/Docs/PyQt4/classes.html">http://pyqt.sourceforge.net/Docs/PyQt4/classes.html</a></li>
</ul>
Après n'hésitez pas à chercher sur Google ;)

Voici les sources du projet présenté dans ce post : <a href="http://blog.nbcorp.fr/wp-content/uploads/2015/07/example-py.zip">example-py</a>

&nbsp;

Voili voilou ! Si vous avez des questions où des remarques, n'hésitez pas à les poster en commentaire !

&nbsp;