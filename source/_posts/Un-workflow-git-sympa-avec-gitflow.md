---
title: Un workflow git sympa avec gitflow
date: 2016-12-13 00:05:24
thumbnailImage: gitflow.jpg
layout: post
tags:
    - Git
    - workflow
    - maintenable
    - devops
categories:
    - Développement
---

Hello,

juste un petit post sur **git flow** que j'utilise dans les gros projets et quand on travaille à plusieurs.
Le principe est simple, des branches et groupes de branches qui ont chacune un rôle spécifique.

<!--more-->

## Description des Branches

La branche `master` va correspondre à  notre environnement de **prod**.

la branche `develop` va correspondre à la version en développement, tous les développeurs doivent commencer ici pour créer une nouvelle feature.

Les branches `feature/*` correspondent à toutes les features. Chaque nouvelle feature est développé dans la branche `feature` puis finish dans la develop.

Les branches `release/*` correspondent à toutes les releases. On utilise une branche release pour préparer et publier une nouvelle version.

Les branches `hotfix/*` correspondent à tous les hotfixes. On utilise une branche hotfix pour créer rapidement un fix et l'appliquer directement sur la branche `master`.

## Git Flow

* [Git flow cheatsheet](http://danielkummer.github.io/git-flow-cheatsheet/)
* [Git flow présentation](http://nvie.com/posts/a-successful-git-branching-model/)
* [Git flow tutoriel (FR)](https://www.grafikart.fr/formations/git/git-flow)

![git flow sketch](git-flow.png)

## Comment utiliser Git Flow dans un projet

1. Respecter et suivre le processus Git Flow
2. Utiliser les commandes Git Flow :
    * ★ Multi-platforme GUI: [GitKraken](http://www.gitkraken.com/)
    * OSX: `brew install git-flow`
    * Linux: `apt-get install git-flow`
    * Windows (cygwin): `wget -q -O - --no-check-certificate https://github.com/nvie/gitflow/raw/develop/contrib/gitflow-installer.sh | bash`
    * Windows GUI: [SourceTree](https://www.sourcetreeapp.com/)
3. En général, on bloque la branche `Master` au développeurs et uniquement les lead-dev ou chef de projet peuvent créer une release.

## GitKraken

La meilleure des solutions pour ne pas se prendre la tête avec Git c'est [GitKraken](http://www.gitkraken.com/)

Voici une cheatsheet qui peut être utile : [GitKraken Cheat Sheet](https://www.gitkraken.com/resources/gitkraken-cheat-sheet)

## Conclusion

Voilà, c'est assez sommaire mais il y a les infos principales pour bien utiliser Git Flow. Je pense que j'éditerai ce post ou en ferait un nouveau sur des cas pratiques rencontrés.

A la prochaine !
