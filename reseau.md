---
layout: page
title: Réseau
permalink: /reseau/
---

Un réseau pour la simulation : "la ligne _Zéro_"

![](../images/logo6.png)

[La ligne Zéro (1996-2000)](#zero)

[La ligne miniZéro (depuis 2022)](#minizero)

[La ligne Un (projet)](#un)

En 1996, j'avais la place pour créer un réseau constitué de 7 modules et d'une coulisse permettant de réaliser une boucle, d'ou le nom de cette ligne : la ligne Zéro. Durant 5 années, j'ai pu tester mes idées concernant la simulation des opérations sous la forme d'un jeu. Après avoir déménagé en 2000, je n'avais plus assez de place pour remonter ce réseau et il a finalement été démantelé. En 2022, j'ai décidé de poursuivre quitte à utiliser un réseau beaucoup plus petit et la ligne miniZéro est alors apparue.

## La ligne Zéro (1996-2000) {#zero}

Mon **réseau imaginaire** représente une ligne SNCF reliant la capitale aux villes de la banlieue dans la partie SUD-EST dans les années 1960-1970, d'une longueur approximative de 150 kilomètres.

Mon réseau traverse quelques départements et une seule gare est effectivement reproduite, mais...  
La partie reproduite est une ligne à voie unique. Il aurait été plus crédible que ce soit une ligne double mais pour des raisons financières, d'espace et de temps, j'ai préféré me limiter pour le moment à une voie unique.  
Il n'y a pas de caténaire, donc pas de locomotive électrique.  
Le matériel de traction est principalement Diesel français, mais il arrive parfois que l'on voit passer des locomotives à vapeur.  
Il existe un trafic de [trains réguliers](/operations/#definitions) de voyageurs et un trafic de marchandises légères. La ligne est jalonnée d'embranchements particuliers vers de petites industries ou des entreprôts.  
Il existe à chaque extrémité une gare importante et au milieu de la ligne deux gares assez importantes pour y justifier un arrêt prolongé des trains, ainsi que la récupération des wagons ramassés par les [trains collecteurs](/operations/#definitions). Les autres gares sont plutôt des gares de passage possédant toutefois des voies de garage et des voies d'évitement.

Le thème que j'ai choisi se caractérise donc ainsi :

*   ligne secondaire en voie unique (réseau imaginaire) ;
*   milieu urbain : Paris, banlieue (je suis parisien d'origine) ;
*   1 gare de passage réelle (gare voyageurs et marchandises) ;
*   2 Embranchements Particuliers ;
*   environnement extérieur : banlieue Est ;
*   1 coulisse (3 voies de triage extérieures).

![](../images/plan.gif)  
Plan du réseau : 4,60 mètres x 2,60 mètres

### La méthodologie de réalisation

Les idées clés de ma méthodologie pour ce réseau sont les suivantes :

*   construction modulaire (modules non normalisés) ;
*   possibilité de réaliser des extensions futures ;
*   réaliser puis améliorer chaque module en plusieurs étapes, par versions successives ;
*   réaliser rapidement une version simple du réseau, permettant de tester puis de valider le concept de jeu.

### La mise en oeuvre de l'exploitation

Pour mon réseau, j'ai défini les critères suivants :

*   nombre d'opérateurs : 1 ou 2 ou 3 ;
*   rôles : conducteurs et/ou chef de la gare et/ou chef de la coulisse ;
*   contrôle manuel des aiguilles (câblage simplifié) ;
*   contrôle manuel des cantons (et signaux associés) ;
*   horloge accélérée (facteur 6 ou 12) ;
*   nombre de circulations simultanées sur la voie unique : 2 ;
*   système de numérotation des trains et wagons ;
*   gestion des wagons ouverts pleins ou vides.

### L'infrastructure

L'infrastructure de mon réseau est décrite par les caractéristiques suivantes :

*   réseau étagère en boucle de 4,60 m x 2,60 m ;
*   largeur des modules : 60 cm ;
*   hauteur des voies : entre 1 m 20 et 1 m 30 ;
*   écartement : voie normale H0 ;
*   dépôt : charbon/fuel, réparation/entretien, remise locos ;
*   construction modulaire (déménagement, photos en extérieur) ;
*   rayon de courbure mini : 55 cm ;
*   câblage simplifié au maximum ;
*   rails PECO code 75 ou 100, aiguilles electrofrog ;
*   fond de décor démontable ;
*   retournement des trains sans pont tournant ;
*   longueur des voies de garage et à quai : 1,20 m ;
*   pas de voie et de bâtiment entre les zones de triage et les opérateurs.

La commande de mon réseau
-------------------------

### Commande traditionnelle {#commande}

J'ai commencé par utiliser deux commandes analogiques traditionnelles : d'abord une commande GMC-UF de GAUGEMASTER achetée en 1990 (et toujours en vente en 2023), c'est un modèle avec asservissement de vitesse très efficace notamment pour les vitesses réduites, ensuite une [commande "maison" avec simulation d'inertie](../images/regula.gif) associée à un générateur 50 khz "maison" pour l'éclairage constant des feux des locomotives.

![](../images/synoptique_multiplexeur.jpg)

La ligne _zéro_ est découpée en trois zones électriques. Un répartiteur permet d'affecter une zone à une commande : il est constitué d'un pupitre muni en façade de commutateurs rotatifs positionnés par rapport au synoptique du réseau (à tout moment, chaque zone ne peut être commandée que par une seule commande).  
 

### Commande digitale

1998 : MRC 2000

J'ai acquis une centrale digitale MRC 2000 de **Model Rectifier Corporation**, ainsi que des décodeurs **ARNOLD** et **LENZ**.

![Commande MRC 2000](../photos/mrc20001.jpg)

J'ai choisi la commande MRC 2000 principalement pour son rapport qualité/prix. J'ai acheté le pupitre avec 3 commandes pour commencer avec l'idée d'acheter plus tard la commande mobile de type "walk-around". A cette époque, j'ai équipé quelques unes de mes locomotives avec des décodeurs ARNOLD 81210 et des décodeurs LENZ LE103 XF.

J'ai réalisé moi-même un boîtier avec un transformateur d'alimentation pour la commande MRC (boîtier bleu sur l'image). La connexion de la commande MRC est très simple : deux fils en entrée pour l'alimentation 15V et deux fils en sortie reliés aux rails. Dans le cas de la commande digitale, le répartiteur électrique présenté ci-dessus devient inutile car le sectionnement électrique du réseau n'est pas nécessaire quand on utilise une commande digitale.

La commande MRC 2000 ne s'interface pas avec un ordinateur. Je ne peux donc pas utiliser un ordinateur pour piloter un train automatiquement.

### Supervision {#supervision}

A l'époque, j'ai utilisé un vieux PC 8086 avec des contacts ILS reliés directement sur le port parallèle.


![Photo du PC de supervision](../photos/victor1.jpg)


La loco du train supervisé ou un wagon est équipé d'un petit aimant permettant d'activer les contacts ILS. Dans cette version de la ligne _zéro_, un contact ILS est disposé en entrée de la gare (Est), un autre en sortie (Ouest).
 

#### Programme de supervision 

Mon programme de supervision temps-réel affiche l'heure courante accélérée, détecte les changements d'état des contacts ILS, et affiche en entrée et en sortie de gare :
*   la gare virtuelle courante (entrée, sortie)
*   l'heure de passage et l'écart entre le tableau horaire et l'heure de passage constatée
*   le **SCORE** courant (en points déjà obtenus)
*   la vitesse moyenne
*   la quantité de carburant restante (en litres)
*   la distance parcourue depuis la gare de départ du scénario


![Copie d'écran du programme de supervision](../images/horloge51.gif)


La commande du programme de supervision s'effectue principalement à l'aide des touches de fonction du clavier, aucune saisie manuelle n'est nécessaire pendant le jeu :

*   F1 : **Pause**, permet éventuellement de stopper momentanément l'horloge accélérée
*   F2 : **Raz**, permet de recommencer le scénario courant au départ
*   F3 : **Enregistrer**, un historique peut être sauvegardé sur disque à tout moment et imprimé par la suite
*   F4 : **Fuel**, permet de simuler un ravitaillement en ajoutant du carburant
*   F5 : **Variables**, permet d'afficher les paramètres de simulation

#### Scénarios

Plusieurs scénarios différents peuvent être exécutés par le programme. Au début d'une scéance de jeu, le scénario est chargé par le programme de supervision. Ce scénario liste toutes les gares à traverser, le sens du parcours (Est,Ouest), les horaires de passage, la distance entre chaque gare, la vitesse maximale autorisée sur tout le parcours, la quantité de carburant au départ et la quantité de carburant chargée à chaque ravitaillement (simulé par la touche fonction F4 du programme).

#### Calcul du score

*   **Passage en gare** : pour chaque gare prévue au scénario, l'entrée rapporte 5 points et la sortie rapporte 5 points. Le fait de ne pas conduire le train jusqu'à sa destination finale est ainsi pénalisant.
*   **Respect des horaires** : pour chaque gare prévue au scénario, une avance ou un retard sur l'horaire retire autant de points que le nombre de minutes d'avance ou de retard. Le fait d'être en avance sur l'horaire est ici considéré comme perturbateur pour le trafic, comme le fait d'être en retard.
*   **Vitesse maximum autorisée** : le dépassement de la vitesse maximum autorisée sur la ligne retire 5 points à chaque contrôle de la vitesse du train, c'est-à-dire en entrée et en sortie de gare. Ainsi, le fait de "trainer" au début du scénario et "accélérer" ensuite pour rattraper son retard peut être une stratégie pénalisante si cela entraîne le dépassement de la vitesse maximum.
*   **Carburant** : enfin, il ne faut pas tomber en panne sèche !

Cet algorithme de calcul du score constitue un premier essai, il doit être amélioré. Déjà, le jeu est intéressant car la valeur courante du score permet d'ajuster le comportement du conducteur dans le but de ne pas avoir de pénalité trop importante, en tout cas supérieure au gain obtenu à chaque passage en gare. A titre indicatif, avec mon [scénario n°1](/operations/#documents), le meilleur score que j'ai obtenu est de 118.

J'ajouterai ensuite d'autres équipements sur le réseau (signaux lumineux, autres capteurs) et d'autres fonctions au programme de supervision pour exploiter ces équipements et en tenir compte dans le score (je progresse par petites étapes pour valider les concepts progressivement).  

## La ligne miniZéro (2022-2025) {#minizero}

Un plateau de 1m20 x 0m85 avec un simple ovale et une seule voie de garage qui reprend et améliore toutes les idées du réseau de 2000.
Il est facilement déplaçable pour jouer n'importe où et faire des démonstrations.
Les mêmes scénarios de jeu précédents sont utilisables. La généralisation du DCC permet toutefois de nombreuses améliorations !


![La ligne miniZéro en 2025](../photos/minizero01.jpeg)


### Station de commande {#dccex}

2022 : Arduino / DCC-EX

Depuis maintenant plusieurs années, les décodeurs DCC NMRA proposent en standard de nombreuses fonctions annexes (au minimum de F0 à F28) ainsi que la sonorisation des locomotives qui est devenue très utilisée. La commande MRC 2000 ne permettant de piloter qu'une seule fonction auxiliaire, un autre système est nécessaire. J'ai décidé de réaliser moi-même une centrale basée sur le logiciel [DCC-EX](https://dcc-ex.com) et la plateforme **Arduino**.  


Hardware :

J'ai réalisé une station de commande complète très simplement en assemblant :
* une carte Arduino Mega 2560
* une carte additionnelle Motor Shield
* une alimentation 18V (5A)

Cette station à une puissance de 2A par défaut (disjoncteur intégré au logiciel DCC-EX). Cela permet de piloter 2 locomotives équipées avec les vieux décodeurs tels que ARNOLD et LENZ qui consomment beaucoup de puissance.

Software :

* ordinateur standard (PC ou Mac) :
    * connecté à la carte Arduino Mega 2560 avec un cable USB (5V et données)
* logiciel open source DCC-EX EX-CommandStation pour Arduino (C++)
* logiciel open source IDE Arduino :
    * initialisation de la carte Arduino
    * Serial Monitor pour piloter la station en utilisant l'API

Pour être compatible avec les anciens décodeurs ARNOLD, il faut utiliser le mode SPEED 28.

### Pilotage

Le pilotage avec les commandes de l'API dans le Serial Monitor n'est pas conçu pour le jeu.
J'utilise principalement le logiciel open source JMRI (Java Model Railroad Interface) avec la configuration suivante :
* ordinateur standard (PC ou Mac) :
    * connecté à la carte Arduino Mega 2560 avec un cable USB (5V et données)
    * connecté au réseau local Wifi
* logiciel JMRI DecoderPro ou PanelPro
* pour la commande mobile de type "walk-around" en Wifi :
    * serveur JMRI WiThrottle
    * application mobile open source Engine Driver pour Android
    * application mobile WiThrottleLite pour iOS 

JMRI permet la gestion complète d'un réseau depuis la programmation des décodeurs DCC jusqu'au pilotage des itinéraires, en passant par les cantons, les signaux, les aiguillages, etc.
Il gère notamment ici pour mes besoins :
* une horloge accélérée
* des scripts d'automatisation tels que l'aller/retour d'une locomotive
* des interfaces natives avec DCC-EX et C/MRI
* des panneaux de contrôle et synoptiques du réseau
* des interfaces techniques (APIs) pour l'intégrer avec d'autres logiciels

Des capteurs tels que des ILS ou des détecteurs de présence par consommation de courant (j'utilise des détecteurs 5556 de Stock87) peuvent être reliés à une carte Arduino. Pour des réseaux qui le nécessitent, la librairie arduinoCMRI permet de réaliser un noeud C/MRI SMINI avec une carte Arduino. Reliée au PC avec un cable USB, JMRI peut ainsi réagir à des changements d'état de boutons et détecteurs et peut actionner des LED et des moteurs d'aiguillage.

### Programme de supervision

Yet Another Railroad Simulator (YARS)

Sans rien perdre des concepts de la version historique de 1998, j'ai développé ce nouveau programme de supervision du jeu (appelé désormais YARS) fondé sur les technologies numériques les plus récentes. La version actuelle (mars 2025) est à considérer comme un premier prototype opérationnel, qui doit évidemment poursuivre son évolution.

Actuellement, YARS s'interface avec le logiciel de pilotage JMRI (Java Model Railroad Interface) de manière à le compléter fonctionnellement. JMRI offre l'avantage de s'interfacer lui-même avec les principales centrales DCC du marché. 
De plus, il offre également à son niveau une interface et un protocole de communication permettant le pilotage des locomotives et accessoires avec divers moyens de télécommande et notamment des applications sur smartphones et tablettes.
En utilisant cette interface, j'ai développé facilement mon propre module au sein de YARS pour commander les locomotives dans les situations de jeu ou cela est utile.
En complément, JMRI affiche facilement l'indispensable horloge accélérée ainsi qu'un synoptique et/ou un tableau de contrôle du réseau.
YARS disposant de son propre serveur web intégré, il peut afficher en temps-réel les informations utiles au déroulement du jeu dans un navigateur standard, sur un voire plusieurs écrans simultanément.


![Copie d'écran du programme de supervision avec JMRI](../images/yars.png)


#### Scénarios

De multiples scénarios sont possibles et sont décrits chacun par un fichier décrivant la liste des gares à parcourir, les horaires de passage, la vitesse maximum autorisée sur la ligne, etc.

#### Calcul du score

Les règles du jeu doivent être respectées, le score est calculé ainsi (version de mars 2025) :

* **Parcours** : chaque entrée en gare rapporte 5 points, de même chaque sortie, il faut aller au bout du parcours.
* **Respect des horaires** : au-delà d'un écart de 2 minutes (tolérance) chaque minute d'avance ou de retard fait perdre 1 point, aussi bien en entrée qu'en sortie de gare.
* **Vitesse maximum autorisée** : chaque km/h dépassant la vitesse moyenne limite autorisée par le scénario entre 2 gares fait perdre 1 point en entrée de gare (pas en sortie).
* **Conduite** :
    * Feux allumés : +100 points
    * Feux éteints par la suite : les 100 points sont perdus, il n'est pas possible de gagner plusieurs fois 100 points en allumant puis en éteignant les feux de la locomotive.
    * Klaxon (F2) en entrant dans la gare : +10 points à chaque coup de klaxon.
* **Carburant** : Une panne de fuel est éliminatoire et le scénario est automatiquement terminé (la locomotive s'arrête toute seule). Il n'est pas possible de ravitailler en roulant, la locomotive doit être à l'arrêt en gare (sachant que l'arrêt en pleine ligne est interdit).

Mon meilleur score est 230 points avec le scénario n°1 allant de Gare du Lion à Melan.

## La ligne Un (projet) {#un}

Après la ligne Zéro (en boucle), la ligne **Un** (en aller/retour).

La ligne 1 en étagère pour simuler le triage des wagons vers les Enbranchements Particuliers (EP).
Un autorail fait des allers/retours en parallèle en passant par la gare.

Le but du jeu est de recevoir un train et de délivrer avec un locotracteur des wagons conformément à une feuille de répartition, en respectant les signaux intermédiaires (tels que les carrés violets), les vitesses modérées, les coups de sifflet obligatoires, les bruitages, les attelages/dételages, les phares, etc. Tout cela permet de calculer un score.

![Ligne 1](../images/ligne1.jpg)

Une difficulté est de contrôler le respect des règles.
Il faut capturer les commandes digitales envoyées au locotracteur.
Il faut aussi vérifier la bonne position des wagons.

Remarque :
Les signaux lumineux doivent être visibles du joueur en toute circonstance pour qu'il puisse les respecter.
Si l'orientation de la voie (et donc des signaux) ne le permet pas, il faut prévoir une répétition des signaux sur un TCO.

Ce projet constituera une extension de la ligne miniZéro en permettant une activité de desserte et triage des wagons de marchandises à l'extérieur de la boucle. De belles heures de jeu en perspective, à suivre...
