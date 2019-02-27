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