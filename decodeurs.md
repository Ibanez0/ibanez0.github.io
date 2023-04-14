---
layout: page
title: Montage des decodeurs DCC
permalink: /decodeurs/
---

L'utilisation d'une commande numérique nécessite l'installation de décodeurs à bord des locomotives.  
L'installation d'un décodeur dans une locomotive nécessite des modifications dans le cablage pré-existant du moteur et des feux, et parfois également quelques modifications pour arriver à loger le décodeur dans la caisse.

Comment choisir son décodeur ?
------------------------------

1.  **Le premier critère est la norme numérique de votre installation**, par exemple DCC NMRA qui est un standard répandu.
2.  **Le deuxième critère est la place disponible à bord de votre locomotive** : il faut compulser les catalogues des fabriquants de décodeurs répondant à la norme de votre installation et choisir un décodeur qui entre dans votre locomotive en longueur, en largeur et en épaisseur ! Il faut donc y trouver une petite place disponible, mesurer le volume maximum qui peut être utilisé et choisir un décodeur plus petit.
3.  Ensuite, mais à ce moment là le choix est déjà réduit, **le troisième critère est le dégré de sophistication du décodeur** au travers des fonctions qu'il offre, par exemple : asservissement de vitesse, protection thermique, protection contre les courts-circuits, fonctions auxilliaires, etc.

  
Selon ma propre expérience, le coût du décodeur se déduit principalement du deuxième critère : si vous avez besoin d'un tout petit décodeur, en général la miniaturisation se paye et votre décodeur sera plus cher, mais a t-on le choix ?

Deux exemples :

*   La 63951 ROCO (version sortie en 1995) est une très bonne machine, avec un gros moteur doux et silencieux, mais en revanche il ne reste que la cabine pour placer un petit décodeur.
*   La 66487 JOUEF (version sortie en 1996) offre très peu de place disponible sous sa carrosserie, sauf au dessus des bogies entre le carter de pignon et la carrosserie, mais la hauteur disponible est réduite.

  
Il est plus rassurant de choisir un décodeur muni de toutes les protections, surtout pour le premier montage, car il resistera mieux en cas de court-circuit ou de surcharge.  
Les fonctions d'accélération et de freinage progressif sont indispensables, elles contribuent au réalisme des manoeuvres et ajoute de l'intérêt à la conduite.

L'asservissement est un plus, il permet des ralentis extrêmes ce qui est particulièrement intéressant pour les manoeuvres mais le coût des décodeurs avec asservissement est plus élevé.  
Toutefois, il faut noter que certaines machines peuvent se passer de l'asservissement, je prendrai comme exemple la 67020 LIMA (version sortie en 1994) qui possède un moteur assez gros et performant pour permettre des manoeuvres à vitesse très réduite avec un décodeur sans fonction d'asservissement. Cela s'explique aussi par le fait que la technologie numérique améliore le fonctionnement des machines parce que le courant traction est rectangulaire (ce qui permet d'avoir un meilleur couple).

Comment installer son décodeur à bord ?
---------------------------------------

### Matériel nécessaire

L'installation d'un décodeur nécessite de savoir faire des soudures à l'étain et donc de posséder un petit fer à souder (30 W maxi). Du petit cable électrique de couleur peut également être nécessaire, du même diamètre que les cables en sortie du décodeur.

### Préparation

Le cablage doit obligatoirement être modifié ce qui se traduit par la suppression de certains cables électriques et éventuellement la coupure de certaines pistes sur les circuits imprimés.  
Il faut bien étudier le schéma électrique avant de procéder à l'installation et faire un schéma du cablage et des circuits imprimés d'origine. Il faut compléter cette étude par une détection systématique des liaisons électriques provoquées par le chassis métalique, qui doivent éventuellement être neutralisées.  
Ensuite, il faut établir le nouveau plan de cablage, déterminer les coupures à effectuer sur les circuits imprimés et bien vérifier avant les travaux qu'il n'y a pas d'erreur dans la conception de ce nouveau cablage.

### Installation du décodeur et cablage du moteur

Maintenant, il faut réaliser les transformations et réaliser le nouveau cablage.  
Il est utile de procéder par étapes, par exemple en ne réalisant en premier que les transformations pour l'alimentation du moteur, sans l'éclairage qui peut être réalisé dans une seconde étape.  
Il faut éviter de couper trop court les fils du décodeur et il faut s'abstenir de déssouder les fils du décodeur dans le but de souder d'autres fils : les soudures sont extrêmement fines donc très difficiles à faire et les composants miniatures sont très fragiles, ils risqueraient de ne pas supporter la chaleur du fer à souder à proximité !  
**Bien vérifier les branchements avant de faire un essai car un court-circuit peut être fatal au décodeur s'il ne possède pas de protection contre les courts-circuits.**  
Retirer les résistances, selfs ou diodes éventuelles qui pré-existent dans la cablage d'origine du moteur.

### Premier essai

Sans même remonter la carrosserie, dès que le moteur est branché, on peut déjà faire un test pour s'assurer que le cablage est correct, en prenant les précautions indiquées par le constructeur (exemple : MRC indique de faire un essai sur un coupon de voie au travers d'une résistance de protection).  
On peut maintenant essayer de replacer la carrosserie, avant même de brancher les feux, pour vérifier que le décodeur entre effectivement dans la place prévue et pour déterminer le passage des cables électriques.

### Cablage des feux

Un des intérêts de la technologie numérique est d'obtenir à la demande l'éclairage permanent des feux avants ou arrières.  
Il est souvent nécessaire d'ajouter du cable pour alimenter les feux car le décodeur possède ses propres fils d'alimentation des feux (3 fils) alors que le cablage d'origine des feux est souvent connecté directement à l'arrivée du courant issue des palpeurs de roues à l'avant et à l'arrière de la machine, ce qui est plus simple pour le constructeur de la locomotive miniature.  
Retirer les diodes qui permettent l'inversion des feux avec le sens de marche car le décodeur se charge maintenant de cette fonction.
