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

![Ligne 1](../images/ligne1.jpg)

## Station de commande

2022 : Arduino / DCC-EX

J'ai décidé de réaliser moi-même une centrale basée sur le logiciel [DCC-EX](https://dcc-ex.com) et la plateforme **Arduino**. Depuis maintenant plusieurs années, les décodeurs proposent en standard de nombreuses fonctions annexes (au minimum de F0 à F28) ainsi que la sonorisation des locomotives. La commande MRC ne permettant de piloter qu'une seule fonction auxiliaire, un changement de technologie était nécessaire. 

![Commande DCC EX JMRI Engine Driver](../photos/dccex1.png)

Hardware :

J'ai réalisé une station de commande complète très simplement en assemblant :
* une carte Arduino Mega 2560
* une carte additionnelle Motor Shield
* une alimentation 18V (5A)

Cette station à une puissance de 2A par défaut (disjoncteur électronique intégré). Cela permet de piloter 2 locomotives équipées avec les vieux décodeurs tels que ARNOLD et LENZ qui consomment beaucoup de puissance.

Software :

* ordinateur standard (Macbook) :
    * connecté à la carte Arduino Mega 2560 avec un cable USB
* logiciel open source DCC-EX EX-CommandStation pour Arduino (C++)
* logiciel open source IDE Arduino :
    * initialisation de la carte Arduino
    * Serial Monitor pour piloter la station en utilisant l'API

Pour être compatible avec les anciens décodeurs ARNOLD, il faut utiliser le mode SPEED 28.

## Pilotage / supervision 

Le pilotage avec les commandes de l'API dans le Serial Monitor n'est pas conçu pour le jeu.
J'utilise principalement le logiciel open source JRMI (Java Model Railroad Interface) avec la configuration suivante :
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
* des automatismes déclenchés par des capteurs (boutons, ILS, etc.)
* des actions sur des composants (LED, moteurs, etc.)

Des capteurs tels que des ILS peuvent être reliés à une carte Arduino.
La librairie arduinoCMRI permet de réaliser un noeud C/MRI SMINI avec une carte Arduino.
Reliée au Mac avec un cable USB, JMRI peut superviser les changements d'état de boutons et capteurs ILS et peut actionner des LED.
