---
layout: page
title: La ligne 1
permalink: /ligne1/
---

UN RESEAU FERROVIAIRE MINIATURE POUR LA SIMULATION

Après la ligne Zéro (en boucle), la ligne **Un** (en aller/retour).


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

Remarque :
Les signaux lumineux doivent être visibles du joueur en toute circonstance pour qu'il puisse les respecter.
Si l'orientation de la voie (et donc des signaux) ne le permet pas, il faut prévoir une répétition des signaux sur un TCO.


## Station de commande

2022 : Arduino / DCC-EX / JMRI

La technologie DCC NMRA est incontournable de nos jours. Il existe plusieurs systèmes prêts à l'emploi mais il est aussi possible de réaliser soi-même une station de commande avec des composants open source.
J'ai choisi le logiciel de commande DCC-EX sur carte Arduino et le logiciel de pilotage JMRI avec ses commandes sur smartphone iOS et Android.

## Supervision

Principe : utiliser l'intelligence artificielle

Le contrôle d'un scénario et du respect des règles peut être réalisé en observant le déroulement du jeu avec une caméra positionnée pour avoir une vue d'ensemble.
Un programme d'intelligence artificielle basé sur un réseau de neurones de type "Object Detector" (Yolo v8 ou RetinaNet) a appris à reconnaitre les locos et les wagons présents à chaque photo avec leur position dans l'image. Un traitement relie la position des éléments sur la photo et la position physique des bâtiments.
Elle peut être positionnée en surplomb, de face ou dans l'axe des voies (ou bien en vue du dessus et en utilisant des marques sur les toitures des wagons si cela peut faciliter la reconnaissance mais cela n'est pas esthétique).

Fonctionnement :
* Caméra : une webcam capture des photos à intervalle régulier (toutes les 5 secondes)
* Normalisation image
* Inférence "Object Detector" : liste des objets détectés
* Détermination de la position des objets sur le réseau modèle (bounding boxes)
* Génération de la log horodatée des positions
* Fusion avec la log horodatée des commandes DCC capturées par JMRI
* Mise en cohérence avec l’historique *
* Calcul des trajets et manoeuvres réalisés
* Calcul du respect des contraintes
* Calcul du score
* Affichage dans JMRI (qui affiche l’horloge, gère le script aller/retour)

(*) entre deux photos, certains objets peuvent temporairement disparaitre en fonction de la reconnaissance par l’IA : il est nécessaire de considérer plusieurs cycles pour compenser.

Pour l'apprentissage du réseau de neurones, il est plus simple que la caméra soit positionnée de face pour éviter d'avoir des perspectives en 3D, dans la mesure ou le jeu de données (images d'entrainement) contient une reconnaissance en 2D vue de face avec des _bounding boxes_ étiquettées rectangulaires en 2D.

Remarque : notons que le cablage du réseau peut rester simple et le plan des voies pourrait même évoluer sans impacter le fonctionnement général. Dans une certaine mesure, cela permet de changer la structure du réseau sans impact sur la supervision et le placement de capteurs.
