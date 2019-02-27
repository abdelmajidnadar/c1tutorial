#                                            Apache Cassandra

## Autour et Audience
Ce tutoriel estt réalisé dans le cadre du UE GLG203. Avant d'entrer dans le vif du sujet, une petite présentation de la base de données Apache Cassandra s'impose pour ceux qui ne la connaissent pas.

## C'est quoi Cassandra?
Apache Cassandra est un système de gestion de base de données (SGBD) de type NoSQL conçu pour gérer des quantités massives de données sur un grand nombre de serveurs, assurant une haute disponibilité en éliminant les points individuels de défaillance. Il permet une répartition robuste sur plusieurs centres de données, avec une réplication asynchrone sans master et une faible latence pour les opérations de tous les clients. 
Aussi il est Orientée colonnes et Décentralisée.
Il est fondée initialement par Facebook, mais en 2008, Facebook transmet ce projet à la fondation Apache
### Les utilisateurs de Cassandra
* Twitter l'utilise pour les données statistiques et la géolocalisation.
* Digg a décidé de réimplémenter entièrement sa gestion de données sous Cassandra.
* Netflix, l'entreprise de streaming TV préfère renoncer aux avantages du relationnel pour l'extensibilité de Cassandra.
* Ebay.
* Instagram.
 
## Pourquoi Cassandra?
* Ne nécessite pas un système de fichiers distribué comme HBase.
* Permet de stocker une large quantité de données.
* Très rapide pour manipuler un volume important de données
* Permet la scalabilité horizontale.
* Assure la disponibilité et la tolérance aux pannes.
Un comparatif de performances fourni par Apache:
    Ecriture: MySQL: 300 ms. Cassandra: 0,12 ms.
    Lecture: MySQL: 350 ms. Cassandra: 15 ms.
    Différences de conception:
      Nombre de colonnes: MySQL: 4096. Cassandra: 2 milliards.

## Théorème CAP
Dans le monde des bases de données NoSQL, on entend souvent parler du Théorème CAP. Ce théorème établit 3 paramètres sur lesquels on peut jouer pour configurer une base de données distribuée :
*    La cohérence ( C pour Consistency)
*    La disponibilité ( A pour Availability)
*    La tolérance aux pannes et aux coupures réseaux ( P pour Partition-tolerance)
Le théorème postule que pour toute base de données distribuée, on ne peut choisir que 2 de ces 3 paramètres, jamais les 3 en même temps. En théorie, on peut donc choisir les couples suivants :
a. Cohérence et disponibilité ( CA ) donc non résistante aux pannes ( P )
b. Cohérence et tolérance aux pannes ( CP ) donc non disponible à 100% ( A )
c. Disponibilité et tolérance aux pannes ( AP ) donc non cohérente à 100% ( C )
Ceci est la théorie. En pratique, on se rend compte que le paramètre P est plus ou moins imposé. En effet, les coupures réseaux cela arrive, c'est inévitable, même si on s'appelle Google... Du coup, le choix se résume en fin de compte à CP ou AP. Cassandra fait clairement le choix de AP pour une tolérance aux pannes et une disponibilité absolue. En contrepartie, Cassandra sacrifie la cohérence absolue (au sens ACID du terme) contre une cohérence finale, c'est à dire une cohérence forte obtenue après une convergence des données.

## Architecture
L'architecture Cassandra s'inspire énormément du papier de recherche Big Table de Google, ainsi que de l'architecture Dynamo d'Amazon. Le moteur de stockage de Cassandra dérive directement de Big Table alors que sa couche de distribution de données s'inspire de l'architecture de Dynamo.
[image](Cassandra_Architecture.png)
Sur le schéma ci-dessus, on distingue la présence de 3 couches métiers :
*    API, responsable de recevoir les requêtes venant des clients sous format Thrift (protocole RPC) ou dans le nouveau format binaire CQL3
*    Dynamo, responsable de la distribution des données entre différents noeuds et du protocole peer-to-peer
*    Base de données, responsable de la persistance des données sur disques
Désormais et jusqu'à la fin de cette série d'articles, on s'intéressera uniquement à la couche base de données, les autres couches techniques feront l'objet d'articles ultérieurs.
