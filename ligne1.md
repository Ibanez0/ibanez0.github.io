---
layout: page
title: La ligne 1
permalink: /ligne1/
---

UN RESEAU FERROVIAIRE MINIATURE POUR LA SIMULATION

Le réseau "la ligne _un_"

Présentation
------------

La ligne 1 en étagère pour simuler le triage des wagons vers les EPs.
Un autorail fait des allers/retours en parallèle.

![Ligne 1](../images/ligne1.jpg)

## Commande

2022 : Arduino / DCC-EX

J'ai décidé de réaliser moi-même une centrale basée sur le logiciel [DCC-EX](https://dcc-ex.com) et la plateforme **Arduino**. Depuis maintenant plusieurs années, les décodeurs proposent en standard de nombreuses fonctions annexes (au minimum de F0 à F28) ainsi que la sonorisation des locomotives. La commande MRC ne permettant de piloter qu'une seule fonction auxiliaire, un changement de technologie était nécessaire. 

Hardware :

![Commande DCC EX JMRI Engine Driver](../photos/dccex1.png)

J'ai réalisé une station de commande complète très simplement en assemblant :
* une carte Arduino Mega 2560
* une carte additionnelle Motor Shield
* une alimentation 18V (5A)

Software :

Cette station de commande est pilotée avec :
* ordinateur standard (Macbook) :
    * connecté à la carte Arduino Mega 2560 avec un cable USB
    * connecté au réseau local Wifi
* logiciel open source DCC-EX EX-CommandStation pour Arduino
* logiciel open source Arduino IDE Serial Monitor (initialisation Arduino)
* logiciel open source JMRI DecoderPro ou PanelPro (Java Model Railroad Interface)
* pour la commande mobile de type "walk-around" :
    * serveur JMRI WiThrottle
    * application mobile open source Engine Driver pour Android
    * application mobile WiThrottleLite pour iOS 

Pour être compatible avec les anciens décodeurs ARNOLD, il faut utiliser le mode SPEED 28.



## Supervision {#supervision}

Des capteurs tels que des ILS peuvent être reliés à une carte Arduino.

La librairie arduinoCMRI permet de réaliser un noeud C/MRI SMINI avec une carte Arduino.

Reliée au Mac avec un cable USB, JMRI peut superviser les changements d'état de boutons et capteurs ILS et peut actionner des LED.
