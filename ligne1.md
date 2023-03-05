---
layout: page
title: La ligne 1
permalink: /ligne1/
---

UN RESEAU FERROVIAIRE MINIATURE POUR LA SIMULATION

Après la ligne Zéro (en boucle), la ligne _un_ (en aller/retour).

Présentation
------------

La ligne 1 en étagère pour simuler le triage des wagons vers les Enbranchements Particuliers (EP).
Un autorail fait des allers/retours en parallèle en passant par la gare.

Le but du jeu est de recevoir un train et de délivrer avec un locotracteur des wagons conformément à une feuille de répartition, en respectant les signaux intermédiaires (tels que les carrés violets), les vitesses modérées, les coups de sifflet obligatoires, les bruitages, les attelages/dételages, les phares, etc. Tout cela permet de calculer un score.

![Ligne 1](../images/ligne1.jpg)

Une difficulté est de contrôler le respect des règles.
Un ILS en entrée et sortie de gare comme pour le réseau de la ligne 0 ne convient pas ici.
Il faut capturer les commandes digitales envoyées au locotracteur.
Il faut aussi vérifier la bonne position des wagons.

## Station de commande

2022 : Arduino / DCC-EX

Depuis maintenant plusieurs années, les décodeurs DCC NMRA proposent en standard de nombreuses fonctions annexes (au minimum de F0 à F28) ainsi que la sonorisation des locomotives qui est devenue très utilisée. La commande MRC 2000 ne permettant de piloter qu'une seule fonction auxiliaire, un autre système est nécessaire.J'ai décidé de réaliser moi-même une centrale basée sur le logiciel [DCC-EX](https://dcc-ex.com) et la plateforme **Arduino**.  

![Commande DCC EX JMRI Engine Driver](../photos/dccex1.png)

Hardware :

J'ai réalisé une station de commande complète très simplement en assemblant :
* une carte Arduino Mega 2560
* une carte additionnelle Motor Shield
* une alimentation 18V (5A)

Cette station à une puissance de 2A par défaut (disjoncteur intégré au logiciel DCC-EX). Cela permet de piloter 2 locomotives équipées avec les vieux décodeurs tels que ARNOLD et LENZ qui consomment beaucoup de puissance.

Software :

* ordinateur standard (Macbook) :
    * connecté à la carte Arduino Mega 2560 avec un cable USB
* logiciel open source DCC-EX EX-CommandStation pour Arduino (C++)
* logiciel open source IDE Arduino :
    * initialisation de la carte Arduino
    * Serial Monitor pour piloter la station en utilisant l'API

Pour être compatible avec les anciens décodeurs ARNOLD, il faut utiliser le mode SPEED 28.

## Pilotage

Le pilotage avec les commandes de l'API dans le Serial Monitor n'est pas conçu pour le jeu.
J'utilise principalement le logiciel open source JMRI (Java Model Railroad Interface) avec la configuration suivante :
* ordinateur standard (Macbook) :
    * connecté à la carte Arduino Mega 2560 avec un cable USB
    * connecté au réseau local Wifi
* logiciel JMRI DecoderPro ou PanelPro
* pour la commande mobile de type "walk-around" en Wifi :
    * serveur JMRI WiThrottle
    * application mobile open source Engine Driver pour Android
    * application mobile WiThrottleLite pour iOS 

JMRI gère aussi :
* une horloge accélérée
* des scripts d'automatisation tels que l'aller/retour d'une locomotive
* des interfaces avec C/MRI
* l'affichage d'un synoptique du réseau

Des capteurs tels que des ILS peuvent être reliés à une carte Arduino.
La librairie arduinoCMRI permet de réaliser un noeud C/MRI SMINI avec une carte Arduino.
Reliée au Mac avec un cable USB, JMRI peut ainsi réagir à des changements d'état de boutons et capteurs ILS et peut actionner des LED et des moteurs d'aiguillage.

## Supervision

Principe : utiliser l'intelligence artificielle

Le contrôle d'un scénario et du respect des règles peut être réalisé en observant le déroulement du jeu avec une caméra positionnée pour avoir une vue d'ensemble.
Un programme d'intelligence artificielle basé sur un réseau de neurones (de type RetinaNet avec la librairie Keras/tensorflow) a appris à reconnaitre les locos et les wagons présents à chaque photo avec leur position dans l'image. Un traitement relie la position des éléments sur la photo et la position physique des bâtiments.
Elle pourrait être positionnée en surplomb, de face ou dans l'axe des voies, ou bien en vue du dessus et en utilisant des marques sur les toitures des wagons si cela peut faciliter la reconnaissance (mais cela n'est pas esthétique).

Fonctionnement :
* Une webcam capture des photos à intervalle régulier (example : toutes les 5 secondes).
* Un programme analyse chaque photo au fur et à mesure, repère la position du locotracteur et des wagons, et insère une ligne de trace horodatée dans un fichier de log.
* Chaque commande passée par la commande DCC-EX produit une trace horodatée dans un fichier de log.
* Les traces sont fusionnées et triées au fur et à mesure.
* Un programme de supervision analyse les traces et calcule un score affiché au joueur.

Remarque : le cablage du réseau peut rester simple et le plan des voix pourrait même évoluer facilement sans impacter le fonctionnement général. Cela permet dans une certaine mesure de changer la structure du réseau sans impact sur la supervision et le placement de capteurs.

Webcam :

* [OpenCV](https://opencv.org) open source maintenu par Intel, une librairie Python existe
* [FFmpeg](https://ffmpeg.org) open source, exécutable en mode commande
* [imagesnap/macos](https://github.com/rharder/imagesnap) open source, mode commande (option répétition)

RetinaNet :

* [Exemple Keras/RetinaNet](https://keras.io/examples/vision/retinanet/) Notebook. Example retinanet.py sur Github
* [retinanet.py / Github](https://github.com/keras-team/keras-io/blob/master/examples/vision/retinanet.py) Contient le code exemple complet par l'équipe Keras, inclut des fonctions de traitement d'image (flipping, resizing).
* [Tutoriel de Jasper Brown](https://github.com/jaspereb/Retinanet-Tutorial) Complet et détaillé
* [How to Train Custom Object Detection Models using RetinaNet](https://medium.com/@van.evanfebrianto/how-to-train-custom-object-detection-models-using-retinanet-aeed72f5d701) Tutoriel Evan Febrianto, les hyperparamètres ne sont pas donnés

Outils IA :

* [Software Installation (Mac on Apple Metal M1)](https://github.com/jeffheaton/t81_558_deep_learning/blob/master/install/tensorflow-install-mac-metal-jan-2023.ipynb) Miniconda, Python, Tensorflow, Jupyter
* [Keras implementation of RetinaNet / Github](https://github.com/fizyr/keras-retinanet) La référence (This repository is deprecated in favor of the torchvision module. This project should work with keras 2.4 and tensorflow 2.3.0, newer versions might break support)
* [LabelImg / Github](https://github.com/heartexlabs/labelImg)




