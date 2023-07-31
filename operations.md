---
layout: page
title: Simulation
permalink: /operations/
---

## Présentation

MODELISME FERROVIAIRE ET SIMULATION

Je suis particulièrement intéressé par l'exploitation des réseaux modèles, surtout d'un point de vue ludique. Ces quelques pages tentent d'expliquer mon point de vue. Dès 1998, j'ai commencé à construire un [réseau](/reseau) pour me permettre de mettre en pratique les idées exposées ici. Cela m'a permis de valider plusieurs solutions et de progresser sur ce sujet.


[Mon projet : un jeu interactif](#presentation)

*   Le but du jeu
*   Les contraintes d'exploitation
*   Les scores

[Les définitions préalables](#definitions)

*   Les sites et bâtiments
*   Les trains

[Le rôle des joueurs](#roles)

*   Le conducteur
*   Le chef de gare ou de zone
*   Le chef du centre de triage caché (coulisse)

[Le scénario](#scenario)

*   Le trafic
*   La simulation du trafic minimal

[La conception du réseau pour le jeu](#conception)

*   Voie unique ou double voie ?
*   Boucle de retournement / topographie du réseau ?
*   Zones cachées (accessibilité) ?
*   Pont tournant ou triangle de voies ?
*   Préparation des trains avant ou pendant (coulisse) ?
*   Allongement artificiel des durées
*   Thème ?
*   Organisation du jeu ?

[La commande du réseau](#commande)

[La supervision et le logiciel de jeu](#supervision)

*   Le programme de supervision
*   Le programme de génération de scénario

[Les documents pour la simulation](#documents)

*   Tableau horaire
*   Liste de répartition des wagons (scénario 1)


## Mon projet : un jeu interactif {#presentation}

La construction d'un réseau entièrement automatique, où l'observateur regarde le mouvement des trains sans rien faire peut constituer un certain défi technique, mais apporte selon moi peu d'intérêt à son constructeur une fois mis au point (à part peut-être la programmation de nouveaux itinéraires).

En revanche, une exploitation à plusieurs joueurs, responsables de conduire leur train d'un point à un autre, avec le respect des contraintes structurelles du réseau et de règles de jeu édictées au préalable retient actuellement mon attention. Cette idée n'est pas nouvelle, loin de là.

Associé à un système de supervision, mon réseau pourrait être considéré comme un jeu interactif, je m'explique : comme pour un réseau entièrement automatique, un ordinateur serait utilisé, non pas pour piloter les trains mais plutôt pour superviser les actions des joueurs et calculer une sorte de score relativement à chaque joueur.

### Le but du jeu

L'ensemble des joueurs doit dérouler un scénario sur une durée donnée en temps accéléré. Le trafic doit être écoulé en respectant les horaires établis :

*   les trains de voyageurs doivent circuler en respectant les départs et arrivées en gare ;
*   les wagons de marchandise doivent être livrés à temps sur leur lieu de destination.

### Les contraintes d'exploitation

Les contraintes qui doivent être respectées par les joueurs sont :

*   signaux (sémaphore, ralentissement, etc.) ;
*   horaires de passage et d'arrivée ;
*   vitesses imposées, que ce soit par les panneaux ou signaux, ou la vitesse maximale autorisée des locos et wagons ;
*   consommations (charbon, eau, fuel) ;
*   pannes simulées ou incidents ;
*   contraintes d'infrastructure (ex : charge maximum des trains) ;
*   procédures d'organisation (ex : remisage des locos) ;
*   coordination entre joueurs ;
*   etc.

L'idée du contrôle des consommations m'est venue du fameux livre "En train avec John Allen" de Linn H. Westcott (traduit en français par Jacques Le Plat), édité par **[Pro Rail International](http://www.ferbach.be/frames_fr/frlivresmain2.htm)** (le Gorre & Daphetid Railroad).

### Les scores

Un ordinateur, connecté au réseau par le biais de capteurs, surveille les actions des joueurs à l'aide d'un logiciel particulier. Il vérifie que les contraintes d'exploitation sont respectées et attribue un score à chaque joueur. Les joueurs qui ne respectent pas toutes les contraintes obtiennent un score plus faible.

## Les définitions préalables {#definitions}

Il est très difficile de reproduire complètement un réseau ferroviaire réel, étant donné l'échelle de réduction (ex : H0=1/87) et la place maximum généralement disponible.

Cependant, lorsque l'on s'intéresse à l'exploitation réaliste du réseau modèle, nous sommes amenés à considérer les flux réels de voyageurs et de marchandises, qui font normalement intervenir de nombreuses gares, de nombreux points de passage et des distances importantes.

Lorsque l'on souhaite simuler les flux réels de voyageurs et de marchandises, il est possible de considérer :

*   le réseau modèle (zone géographiquement délimitée) ;
*   l'extérieur du réseau, simulé alors par une "**coulisse**" (les américains appellent cette zone "fiddle yard").

Cette coulisse correspond à la gare cachée de certains réseaux modèles, qui permet de cacher les trains pour les faire apparaître aux observateurs au moment voulu. Contrairement à une gare cachée, nous considérons la coulisse comme entièrement visible pour autoriser sa gestion par un opérateur :

*   triage des wagons ;
*   formation des convois ;
*   remplissage ou vidage des wagons (simulation de l'activité des usines extérieures).

L'idée de coulisse active m'est venue d'un article intitulé "Flexible operation with a fiddle yard" by John Ozanich dans Model Railroad Planning 1995, un magazine annuel publié par **[Kalmbach Publishing Co.](http://www.kalmbach.com/)** (USA).

### Les sites et bâtiments

Différentes sortes de sites et bâtiments apportent un intérêt pour l'exploitation. Ces sites sont à l'origine des flux de voyageurs et de marchandises, donc à l'origine du trafic que l'on cherche à reproduire :

*   les **gares de voyageurs** ;
*   les **gares de marchandises** (halles à marchandises et voies associées) ;
*   les **Embranchements Particuliers** (EP : usines, etc.) ;
*   etc.

D'autres sites permettent de simuler les contraintes d'organisation de la société de chemin de fer :

*   les installations ferroviaires annexes (dépôts de locomotives, etc.) ;
*   les centres de triage ;
*   etc.

### Les trains

Les trains dits "**réguliers**" relient les gares et sont du type :

*   train de marchandises ;
*   train de voyageurs et autorails ;
*   train mixtes, composés de voitures et de wagons (MV).

Les trains dits "**collecteurs**" collectent puis rassemblent à la gare la plus proche tous les wagons des usines environnantes qui doivent être expédiés vers l'extérieur.

L'idée des trains collecteurs m'est venue du fameux livre "En train avec John Allen" de Linn H. Westcott (traduit en français par Jacques Le Plat), édité par **[Pro Rail International](http://www.ferbach.be/frames_fr/frlivresmain2.htm)** (le Gorre & Daphetid Railroad).

## Le rôle des joueurs {#roles}

Un rôle est attribué à chaque joueur :

*   conducteur ;
*   chef de gare ou de zone ;
*   chef du centre de triage caché (coulisse).

### Le conducteur {#conducteur}

Un conducteur est responsable d'un train de voyageurs ou de marchandises.

Les tâches d'un conducteur sont les suivantes :

*   prendre en charge sa machine au dépôt (cf. procédure) ;
*   conduire son train de son origine à sa destination ;
*   respecter sa fiche horaire ;
*   respecter le code de la route ferroviaire ;
*   gérer sa loco (consommations, ravitaillement) ;
*   gérer les signaux et aiguilles devant et derrière son train ;
*   gérer son train (dépose et enlèvement de wagons aux points de passage) ;
*   laisser sa machine au dépôt (cf. procédure) ;
*   coordonner ses actions avec celles des autres joueurs.

### Le chef de gare ou de zone {#chef_gare}

Le chef de gare ou de zone est responsable de tout ce qui se passe dans sa gare ou sa zone. Ses tâches sont les suivantes :

*   gérer le train collecteur de marchandise ;
*   gérer les voies en gare ;
*   gérer les signaux et aiguilles des voies en gare ;
*   gérer les locotracteurs dédiés à la répartition des wagons ;
*   gérer la halle à marchandises.

### Le chef du centre de triage caché (coulisse) {#chef_triage}

Les tâches du responsable de la coulisse sont les suivantes :

*   réceptionner les trains ;
*   mélanger et trier les wagons pour simuler le trafic extérieur à la zone maquettée ;
*   gérer le chargement des wagons ;
*   expédier les trains (application des horaires) ;
*   gérer le trafic automatique.

## Le scénario {#scenario}

Le scénario définit les **mouvements** des trains nécessaires à l'écoulement du trafic par le réseau de la société ferroviaire.

### Le trafic

Nous considérons que le trafic est engendré par :

*   le déplacement des voyageurs entre les gares ;
*   l'acheminement de marchandises entre les gares et/ou les EP.

La forme du scénario dépend du type de jeu souhaité :

*   dans le cas le plus simple pour les joueurs, le scénario établit de manière exhaustive une liste chronologique des mouvements, chacun étant précisément daté ;
*   dans le cas le plus fastidieux, le scénario établit les demandes de trafic ; ce sont les joueurs qui doivent composer les trains permettant d'écouler ce trafic.

Le premier cas impose uniquement des tâches d'exécution. Le second cas est proche de la réalité, il nécessite des tâches de planification, qui s'imposent effectivement aux sociétés ferroviaires.

Pour mon réseau, je souhaite que le trafic se décompose ainsi :

*   trafic majoritaire : marchandises légères soumises au triage ;
*   trafic minoritaire : voyageurs à horaires fixes.

### La simulation du trafic minimal

Lorsque peu de joueurs sont présents, voire dans le cas extrême d'un seul joueur, il est intéressant de simuler un trafic minimal. Il peut être simulé par un ordinateur de commande qui assure alors les mouvements à la manière d'un joueur, ou même de plusieurs.

On s'aperçoit que si l'ordinateur assure tous les mouvements, on se retrouve alors dans le cas d'un réseau entièrement automatique, ce qui n'est pas le but recherché.

Il est possible d'exploiter cette idée avec peu de moyens : le simple aller-retour d'un autorail (ou d'une rame réversible) du réseau vers l'extérieur, cadencé par un mécanisme électronique voire électrique (relais, condensateurs) constitue déjà un trafic voyageurs minimal à horaires régulier.

Il est également possible, dans le cas d'un réseau en boucle, de faire tourner en permanence un autorail à vitesse réduite, pour simuler un trafic voyageurs minimal à horaires régulier (cette idée m'est venue d'un article intitulé "Continuous running on a point-to-point railroad" dans Model Railroad Planning 1996, un magazine annuel publié par **[Kalmbach Publishing Co.](http://www.kalmbach.com/)** - USA).

## La conception du réseau pour le jeu {#conception}

La réalisation d'un réseau où l'on veut simuler des opérations réalistes nécessite une conception attentive de son plan de voies, pour permettre la mise en oeuvre des concepts clés d'exploitation.

Voici par exemple quelques questions d'importance :

### Voie unique ou double voie ?

Une voie double permet de faire circuler plus de trains simultanément ce qui peut occuper plus d'opérateurs. Elle permet par exemple de faire tourner un train en boucle simulant alors un trafic permanent dans lequel un opérateur doit insérer son train sans rien perturber. Elle permet aussi des circulations plus complexes.

### Boucle de retournement / topographie du réseau ?

Trois exemples :

1) Un réseau en forme d'os dans un schéma en double voie (sans boucle de retournement) facilite l'aller et le retour continu des trains par les gares de passage : on a plus de trafic en ligne et une gestion plutôt simple, il faut respecter l'espacement. Pour certains wagons, il faut modifier leur chargement (les vider ou les remplir) pour simuler l'activité.

2) Un réseau en forme d'os en voie unique impose deux boucles de retournement : on a moins de trafic en ligne et une exploitation compliquée par la gestion de l'occupation de la voie (sans compter les problèmes électriques).

3) Un réseau circulaire, même assez grand autour d'une pièce, ne permet pas de gérer facilement l'aller retour des trains (ils passent naturellement toujours dans le même sens dans les gares) : il est alors utile d'avoir une coulisse permettant de retourner les trains avec une 0-5-0 (main de cinq doigts) ou une autre machine mais cela prend du temps, ça casse la fluidité du trafic et ça rend disproportionnées les durées de triage relativement aux durées des parcours.

### Zones cachées (accessibilité) ?

Il faut éviter les zones inaccessibles pour pouvoir intervenir partout sur le réseau, en cas de déraillement, en cas d'encrassement des voies nécessitant des interventions manuelles.

### Pont tournant ou triangle de voies ?

En l'absence d'un dispositif pour retourner les trains dans le cas de certaines topologies (ex : réseau circulaire) il faut accepter que les trains ne puissent pas effectuer des allers-retours.  
Par ailleurs, un pont tournant nécessite moins d'espace qu'un triangle de voies

### Préparation des trains avant ou pendant (coulisse) ?

Le garage des trains en attente dans une gare cachée inaccessible interdit de les retourner et d'en modifier la composition. C'est une des raisons qui justifie une coulisse séparée du réseau mais ouverte pour qu'un opérateur puisse y intervenir (avec une 0-5-0 !).

### Allongement artificiel des durées

Nos réseaux étant le plus souvent assez comprimés, les distances entre les gares sont très courtes (quelques mètres). En jouant sur le facteur d'accélération du temps, à l'aide d'une horloge accélérée, on simule des [tableaux horaires](/operations/#documents) réalistes (avec un facteur 12, 5 minutes réelles sont considérées comme 1 heure simulée et 1 mètre réel représente 1 kilomètre simulé), mais il n'empêche que les durées réelles des trajets, celles qui permettent aux opérateurs de préparer les tâches suivantes, sont courtes : 10 mètres réels de voie représentent 10 kilomètres parcourus approximativement en 30 secondes réelles à une vitesse simulée de 60 kilomètres / heure. Ca ne laisse pas beaucoup de temps pour basculer les aiguilles, dégager les voies, se préparer aux mouvements suivants, le tout sans se tromper !

L'utilisation d'une spirale permet de franchir des dénivelés importants et permet d'allonger la durée d'un trajet entre deux points : cela laisse un peu de temps aux opérateurs.

### Thème ?

Le choix du thème a un impact très important sur les possibilités de jeu. Par exemple, le trafic dans les zones industrielles est important mais surtout composé de trains de marchandises, tandis que le trafic en campagne sur une ligne secondaire peut être moins important mais plus varié, avec des trains marchandises / voyageurs (MV) et des autorails.

### Organisation du jeu ?

*   nombre d'opérateurs et rôles associés ?
*   degré d'assistance ou d'automatisme : contrôle manuel ou automatique des aiguilles, des cantons, des signaux ?
*   nombre de circulations simultanées ?
*   formalisation du jeu : quels formulaires, quel système de numérotation des véhicules, gestion des wagons ouverts pleins ou vides ?

## La commande du réseau {#commande}

De quoi a t-on besoin pour exploiter son réseau dans de bonnes conditions de jeu ?

Dans le désordre :

*   une commande mobile de type "walk-around" pour chaque joueur ;
*   un câblage simplifié au maximum ;
*   un partitionnement électrique très simple du réseau en zones distinctes ;
*   une commande de train gérée par un ordinateur, en plus des commandes des joueurs ;
*   une alimentation avec asservissement de vitesse pour chaque commande (permet des ralentis extrêmes même pour les locos peu performantes) ;
*   l'éclairage constant des feux de locos ;
*   un Tableau de Contrôle Optique (TCO) sur écran d'ordinateur.

Il faut que les opérateurs soient déchargés des tâches de gestion de l'affectation des commandes aux cantons.

J'ai examiné principalement trois types de systèmes :

*   les commandes traditionnelles (transfo classique) ;
*   les commandes de conduite sélective (ex : CS 90, JAO) ;
*   les commandes digitales avec décodeur à bord des locomotives (ex : Digital-Plus de LENZ).

**Tableau comparatif :**  

| Commande classique | Commande digitale |
|--------------------|-------------------|
| Il faut assembler des systèmes disparates parfois incompatibles, exemple : la commande GAUGEMASTER GMC-UF est incompatible avec le générateur 50 khz car tout composant électrique (bobine de découplage) intercalé dans le câblage perturbe le fonctionnement de l'asservissement de cette commande. | Une seule centrale "équivaut" à plusieurs transformateurs classiques déjà sophistiqués (avec des décodeurs à simulation d'inertie et asservissement) et intègre de plus la fonction d'éclairage constant. Il faut installer un décodeur dans chaque locomotive. |
| Le câblage devient rapidement complexe avec tous les problèmes associés (de nombreux modélistes ont déjà exprimé les difficultés rencontrées et les solutions possibles). | Le câblage est réduit au minimum par conception du système digital. |
| Pendant une séance de jeu, l'exploitation des zones électriques nécessite presque un opérateur dédié si on veut éviter les courts-circuits ou les mauvaises surprises. Par exemple, pris dans l'action, il n'est pas rare de voir un train s'arrêter brutalement en changeant de zone électrique à cause d'une mauvaise affectation de la commande de l'opérateur.| Il n'y a pas de zone électrique, donc pas d'exploitation associée. |
| Sur un réseau assez petit, il est impossible de faire se suivre deux trains : cela nécessite alors un vrai bloc système ou une commande sélective par exemple. Il est impossible de gérer à la main la vitesse des trains en même temps que l'affectation des commandes aux zones électriques (en particulier quand les zones sont courtes), sans compter les autres actions à mener (commande des aiguilles, préparation des manoeuvres, etc.). | Il est facile de se faire suivre plusieurs trains, chacun ayant sa commande de vitesse. |
| Il est impossible de venir accoupler une machine avec une autre à l'arrêt (sauf si l'accouplement vient à être effectué à un endroit où il existe une frontière entre deux zones électriques). | L'accouplement est possible n'importe où, ensuite la conduite des deux machines nécessite de les commander en parallèle (pousser les deux curseurs en même temps) ou d'affecter le même code numérique aux deux machines.|

Du point de vue de l'exploitation, la solution de commande classique limite les possibilités et complique le jeu pour les opérateurs. 

Au titre des avantages, le prix d'une commande traditionnelle reste faible, en tout cas il est encore assez inférieur à celui d'une commande digitale prête à l'emploi. En outre, les locomotives n'ont pas besoin d'être modifiées (par exemple, être équipées de décodeurs). L'utilisation de l'éclairage constant reste tout de même un problème car il n'est pas si facile que ça à mettre en oeuvre.

Les commandes de conduite sélective ont pour moi l'inconvénient de ne pas être fondées sur une norme standardisée reconnue par les constructeurs. Leur prix reste assez élevé.

Au contraire, la plupart des commandes digitales sont désormais basées sur le standard DCC de la **[NMRA](http://www.nmra.org/)** ce qui constitue un gage de pérennité et de diminution des prix de par le jeu de la concurrence. Pour les passionnés d'électronique et d'informatique, il est possible de construire une commande DCC à partir de composants open source pour le dizième du prix d'une commande du marché.

## La supervision et le logiciel de jeu {#supervision}

Le système de supervision impose l'utilisation d'un ordinateur et d'un logiciel. Il est également possible de réaliser un système entièrement électronique, par exemple avec des cartes Arduino ou Raspberry Pi, mais il n'est pas aussi facilement évolutif.

### Le programme de supervision {#prog_supervision}

#### Les fonctions du programme de supervision

Le mode de fonctionnement recherché nécessite principalement l'entrée de signaux provenant soit du réseau vers l'ordinateur, soit du clavier.

Le programme de supervision est chargé de :

*   afficher l'heure accélérée ;
*   afficher la gare courante ;
*   contrôler le chemin emprunté par les trains ;
*   contrôler le respect des consignes de vitesse ;
*   contrôler le respect du tableau des horaires (arrêts aux stations prévues, heures d'arrivée, heures de départ) ;
*   simuler la consommation des locomotives et contrôler le réapprovisionnement (bouton ou clavier), le cas échéant, il est nécessaire de dépêcher sur place une autre locomotive, ce qui perturbe le trafic ;
*   commander les signaux et contrôler le respect des signaux ;
*   commander l'éclairage du réseau (jour, nuit) ;
*   commander la coupure d'alimentation de certaines sections pour simuler des pannes de carburant ou des avaries du matériel ;
*   calculer le score ;
*   etc.

#### Le matériel électronique et informatique

**La solution matérielle permettant de réaliser un système de supervision avec les fonctions décrites précédemment consiste en :**

En 1998 :

*   un ordinateur PC avec un port parallèle et un port série (ex : mon vieux 8086) ;
*   un boîtier d'interface avec entrées isolées et sorties sur relais à brancher sur le port série ou parallèle du PC (ex : modèle ORD102 prêt à l'emploi de la société [ELECTROME](http://www.jclelectrome.fr/)) ;
*   quelques contacts ILS disposés aux endroits stratégiques du réseau et en entrée/sortie de la gare (remarque : une seule locomotive peut alors être facilement contrôlée) ;
*   l'allumage et l'extinction progressive de la lumière, en douceur, peut être réalisée par un module électronique (ex : kit K2657 de Velleman-kit environ 25 Euros TTC).

En 2020 :

* un ordinateur PC avec ports USB et/ou WiFi ;
* des circuits électroniques d'interface peuvent être réalisés facilement avec Arduino (ou Raspberry Pi) par exemple.

**Quelques précisions :**

Cette solution de supervision offre l'avantage d'être indépendante du système d'alimentation qui peut être classique ou numérique.

Dans mon cas, il faut noter que le réseau est constitué d'une voie unique de longueur assez limitée (12 mètres en boucle) et d'une gare unique. Je souhaite pourtant réaliser des scénarios passant par plusieurs gares. J'ai donc adopté le principe que l'unique gare réelle peut représenter plusieurs gares fictives. Tout scénario passant virtuellement par plusieurs gares boucle par l'unique gare réelle existante sur le réseau. Pour aider les joueurs, l'ordinateur affiche alors le nom de la gare courante, les joueurs ne doivent pas tenir compte du nom inscrit sur le bâtiment de la gare réelle (là encore, l'ordinateur apporte une aide).

Les contacts ILS ne permettant de distinguer de manière simple qu'une seule locomotive, les joueurs conducteurs doivent réaliser le plan prévu au tableau horaire chacun leur tour pour que le programme puisse calculer leur score (cette contrainte n'enlève pas d'intérêt au jeu car plusieurs joueurs sont requis pour exécuter ce type de scénario : un conducteur, un contrôleur pour les aiguillages et un chef de gare). Toutefois, le système reste évolutif car il faut noter que l'utilisation d'un système de reconnaissance de type code à barre à la place des ILS permettrait alors au programme de gérer simultanément plusieurs trains, donc plusieurs joueurs.

### Le programme de génération de scénario {#prog_generation}

Lors de mes premières recherches en 1996, je ne trouvais quasiment pas de logiciel pour générer des scénarios de jeu qui soient indépendants de produits spécifiques tels que, par exemple, les commandes numériques avec interface ordinateur. Ayant les compétences nécessaires, j'ai donc décidé de réaliser mon propre programme pour me faciliter la mise au point de scénarios de jeu, selon des paramètres tels que :

*   la liste des locomotives, wagons et voitures en jeu ;
*   les durées des trajets entre les zones et la durée des arrêts en gare ;
*   les heures et la durée du scénario ;
*   etc.

Je voulais un programme indépendant de la commande des trains, assez général et paramétrable pour s'adapter à différentes situations de jeu. J'étais conforté dans cette idée par la lecture de plusieurs articles présentant des réseaux réalisés par des américains qui organisaient des séances de jeu à grande échelle.

En 1997, j'ai effectivement réalisé un prototype de programme de génération pour me permettre de générer des scénarios pour mon plan de voies. J'ai réalisé ce programme en une dizaine de jours en langage lisp sur mon vieux PC. Ce programme génère deux tableaux : la liste des véhicules avec leurs mouvements horodatés, et la liste chronologique des mouvements. La première liste donne sur une unique page A4 les mêmes informations que les fameux _way bills_ des réseaux américains (feuille de route de chaque wagon). Mes conclusions sur cette expérience sont à ce jour les suivantes : à moins d'être un club organisant fréquemment de nouveaux scénarios dans des conditions changeantes (ex : plan de voies modifiable selon l'agencement de modules), il est plus rapide de calculer ses scénarios avec un outil de saisie tel qu'un traitement de texte ou mieux un tableur que de paramétrer un programme. Le plan de voies du réseau contraignant fortement les possibilités pour les scénarios, dans un premier temps il faut déterminer les types de scénarios possibles et ensuite faire varier les paramètres indépendants du plan de voies (ex : type de trafic, horaires, règles, etc.).

Maintenant, **j'utilise un tableur pour mettre en forme un [tableau horaire général (_timetable_)](#timetable) et des [listes de répartition des wagons (_switch list_)](#switchlist) pour chaque scénario.**

L'intelligence nécessaire pour construire des scénarios pertinents et intéressants avec de nombreux paramètres possibles est difficile à mettre dans un programme de calcul automatique. La réalisation d'un programme personnalisé n'est pas rentable si le nombre de scénarios à réaliser est potentiellement faible. L'utilisation d'un programme existant apporterait un plus à condition qu'il soit suffisamment générique pour s'adapter aux nombreux cas possibles et donc ainsi aux cas qui nous préoccupent. Finalement, l'utilisation d'un tableur constitue peut-être un bon compromis en permettant de réaliser certains calculs (somme des durées, longueurs, poids, calcul de moyennes, etc.) qui facilitent le travail du concepteur et en permettant une mise en page totalement personnalisée.

## Les documents pour la simulation {#documents}

### Tableau horaire {#timetable}

Les tableaux horaires décrivent les trajets des trains avec les horaires associés. En fonction des jours de la semaine et plus généralement du calendrier, ils décrivent sous la forme d'une matrice la liste des gares traversées par chaque trajet, les heures de départ et d'arrivée, les durées d'arrêt aux correspondances, les distances parcourues, etc.

Pour commencer mes essais, j'ai conçu cette première version d'un tableau horaire simple, relatif au trafic de convois de marchandises. J'ai ajusté les horaires après les premiers essais sur mon réseau.

Les horaires sont liés à l'utilisation de mon horloge accélérée (d'un facteur 12) et à la mesure des distances représentées par le réseau, compte-tenu de l'échelle de réduction au 1/87 et du facteur d'accélération. Pour mémoire, avec ces deux paramètres, un mètre réel de voie du réseau représente environ un kilomètre fictif. Le scénario commence et se termine dans la gare de triage en coulisse. La distance entre deux gares s'avère être de 12 Km correspondant à la distance parcourue à l'échelle compte tenu du facteur d'accélération (12 mètres représentent environ 12 Km). Mon programme de supervision sur PC, enregistre chaque passage du train à l'entrée de la gare et calcule sa distance parcourue et sa vitesse moyenne sur le parcours. Les vitesses entre deux gares constatées lors de mes premiers essais varient entre 40 Km/heure et 60 Km/heure à l'échelle. Il est également nécessaire d'étalonner la commande du train pour que le conducteur sache quelle est sa vitesse à chaque cran du bouton de commande.

Pour ce premier tableau, je me suis inspiré du formulaire de type _Timetable_ présenté par Jack Burgess pour son [Yosemite Valley Railroad](http://www.yosemitevalleyrr.com). Je l'ai réalisé avec un tableur standard.

![Tableau horaire / Timetable (20 Ko)](../images/timetable.gif)

Les temps indiqués correspondent aux arrêts en gare. Lorsque deux heures sont indiquées pour une même gare (en gras), elles correspondent aux heures d'arrivée et de départ, sinon lorsqu'une seule heure est indiquée, le temps d'arrêt standard est de 3 minutes (le temps de décharger le courrier...).

J'ai pu déjà constater qu'il n'est pas si facile de tenir l'horaire car tout écart est démultiplié par le facteur d'accélération utilisé. Cela m'amène à penser qu'il faudrait maintenant que je réalise des essais avec un facteur 6, comme certains modélistes. Dans tous les reportages que j'ai pu lire sur ce sujet, les modélistes utilisent généralement un facteur de 6, 10 ou 12.

Autre point important, on ressent une certaine dilatation du temps pour tous les mouvements qui doivent être effectués en gare car là on doit réaliser les manoeuvres sur une échelle de temps non accélérée (on ne peut pas déplacer les wagons à toute vitesse) et on constate sur le tableau horaire des durées de une à deux heures pour manoeuvrer seulement quelques wagons.

A l'avenir je vais essayer d'autres horaires avec plus de variété dans les types de relations.

### Liste de répartition des wagons (scénario 1) {#switchlist}

Les listes de répartition des wagons indiquent les mouvements de wagons de marchandises a réaliser pour répondre aux besoins des clients.
Les wagons, vides ou remplis, sont déplacés d'un endroit à un autre qui sont par example une entreprise ou une zone de triage.
Une telle liste de répartition précise la date d'exécution, le tableau horaire utilisé, et pour chaque wagon à déplacer : son identifiant, son lieu de départ, son lieu d'arrivée.

![Liste de répartition des wagons / Switchlist (10 Ko)](../images/switchlist.gif)

Pour un même tableau horaire, il est possible de réaliser plusieurs scénarios en fonction des wagons et des mouvements concernés. J'ai commencé modestement, avec un scénario simple n'incluant que quelques wagons. De plus, ce sont des couverts ou des citernes, donc la gestion de leur chargement n'est pas à faire dans ce scénario.

Il faut prévoir l'organisation des mouvements dans les gares avant de les atteindre. En effet, il faut prévoir l'occupation des voies et la disponibilité de locomotives sur place pour effectuer la livraison des wagons aux embranchements particuliers.

J'utilise une désignation des wagons qui permet de les repérer facilement par leur type et leur couleur. Les lieux d'origine et de destination sont indiqués par les bigrammes des gares, tels qu'indiqués sur le tableau horaire. Les wagons sont triés en fonction de leur lieu de départ.

Pour ce formulaire, je me suis inspiré du formulaire de type _Switchlist_ présenté par Jack Burgess pour son [Yosemite Valley Railroad](http://www.yosemitevalleyrr.com), ainsi que des informations des formulaires proposés par le logiciel Ship It! Car Cards Version 1.0 from Albion Software. Je l'ai réalisé avec un tableur standard.

Je vais essayer d'autres scénarios en y ajoutant des mouvements à réaliser dans ou entre les gares. Avec la commande digitale, je peux faire évoluer simultanément un train dans chaque sens, ou bien un train collecteur avec un train régulier.
