---
title: 'OHA : Open Home Automation'
date: 2015-02-15 11:25:47
layout: post
tags:
    - API
    - Arduino
    - Automation
    - Connecté
    - domotique
    - Home
    - IoT
    - OHA
    - Open
    - Projet
    - PRT5
    - Python
    - RF433
categories:
    - Domotique
comments: true
---
En dernière année d'école d'ingénieur, nous avions la possibilité de réaliser un projet technique sur le sujet de notre choix. Il se trouve que j'avais depuis longtemps envie de développer ma propre solution de domotique. En effet, je regardais souvent du côté de [S.A.R.A.H.](http://blog.encausse.net/s-a-r-a-h/) ou encore [Gladys](http://gladysproject.com/accueil). Il en existe plein d'autre qui offre souvent la couche logicielle et qui sont Open Source mais je n'ai jamais vraiment trouvé de solution complète Open Hardware et Open Source.

<!--more-->

Mais dans un premier temps, un petit rappel sur ce qu'est la domotique :

*La domotique est l'ensemble des techniques de l'électronique, de physique du bâtiment, d'automatisme, de l'informatique et des télécommunications utilisées dans les bâtiments, plus ou moins "interopérables" et permettant de centraliser le contrôle des différents systèmes et sous-systèmes de la maison et de l'entreprise (chauffage, volets roulants, porte de garage, portail d'entrée, prises électriques, etc.).*

**Mais qu'est ce que OHA :**

Open Home Automation est un projet de domotique Open Source innovant qui permettra de contrôler les équipements de la maison, volets, lampes, chauffages par l'intermédiaire de son smartphone, tablette, PC, Laptop, etc. OHA propose une solution domotique qui ne nécessitera pas de changement important dans les installations de la maison, comme c'est le cas pour les solutions domotiques du marché. De plus chacun (particulier ou entreprise) pourra construire et ajouter son propre équipement connecté grâce à la Centrale Intelligente OHA qui détecte automatiquement les nouveaux équipements domotiques compatibles. OHA n'est pas qu'un simple système domotique propriétaire, c'est un univers d'objets connectés où chacun peut ajouter le sien.


Pour OHA, nous voulions développer un système ouvert offrant une bonne base pour toutes les applications de domotique. Voici un schéma fonctionnel du système :

![schéma principale](/nbcorp-blog/images/schema-principale.png)

Cette article présentera globalement le système mais je ferais sûrement d'autre article plus technique qui détaillera les différentes parties du système.

Nous êtions une équipe de 4 personnes (2 personnes sur le logiciel API+client web et 2 personnes sur le reste : développement du daemon python + des modules Arduino). Ce projet a duré environ 6 mois (de Septembre 2014 à Janvier 2015) et nous nous étions fixé comme objectif d'avoir un serveur communicant avec un module simple de lampe connectée.

Voici la maquette finale du système :

![oha-maquette-1](/nbcorp-blog/images/oha-maquette-1.jpg)

Voici quelques vidéos (playlist Youtube) de démonstration qui montrent les fonctionnalités de base de système.

<iframe allowfullscreen="" frameborder="0" height="315" src="https://www.youtube.com/embed/videoseries?list=PLsTK3RYVBmuDBkJ-arTuKlfv2TFFZgNXX" width="560"></iframe>


Et sinon comme le système est Open Source, retrouvez tous nos documents sur Dropbox et le code sur notre serveur git :

* OHA Dropbox : <https://www.dropbox.com/sh/elvth88n0mhhb0w/AADJKHIOZmS7qmZaeL1MDOVha?dl=0>
* git OHA Web client : <http://git.nbcorp.fr/oha/oha-web-client>
* git OHA API : <http://git.nbcorp.fr/oha/oha-api>
* git OHA Python Core : <http://git.nbcorp.fr/oha/oha-python-core>
* git OHA Module Core : <http://git.nbcorp.fr/oha/oha-module-core>

 Voilà, ça sera tout pour cette article d'introduction, je vais refaire d'autre article sur le sujet pour présenter l'architecture globale du système, les différents composants (API, Daemon, ...).

Si vous avez des questions, n'hésitez pas à les poser en commentaire ;)
