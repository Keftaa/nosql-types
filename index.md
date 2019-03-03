
## Introduction

À la fin de votre lecture de cet article, vous aurez fait connaissance du système de gestion de bases de données le plus populaire de chaque type. Cette introduction plutôt pratique que théorique, vous aidera à comprendre concrètement le fonctionnement et les cas d'utilisation de chaque différent type de NoSQL. 

Cet article présume une connaissance générale des bases de données relationnelles (RDBMS) et bien évidemment du langage SQL.

## Les types de bases de données non-relationnelles

De base, il existe 4 types de bases de données NoSQL :
1. Magasin clé-valeur : la plus simple des versions de NoSQL. Elle consiste d'un mapping de la clé à la valeur.

2. Magasin à colonnes larges : permet de stocker des données en colonnes au lieu de lignes.

3. Bases de données en document : une structure de base de données NoSQL très similaire au format JSON.

4. Bases de données graphiques : utilise les structures de graphes pour les requêtes sémantiques avec des nœuds, des arêtes et des propriétés pour représenter et stocker des données.

## Premier type : clé-valeur

### SGBD le plus populaire
Le plus populaire des systèmes de gestion de bases de données non-relationnelles clé-valeur est Redis. J'utiliserai "Redis" et "BDD clé-valeur" de façon interchangeable.

### Pourquoi Redis ?
Redis est très rapide puisque ses données sont stockées en mémoire vive (avec possibilité de persistence bien-sûr !). Redis (et les BDD clé-valeur) sont comme leur nomenclature l'indique, simplement des clés et des valeurs - donc sans la pénalité de la performance des "relations" dans les bases de données relationnelles.


### Cas d'utilisation
Redis est utile si votre structure de données est simple et non relationnelles. Prenons l'exemple d'un jeu vidéo à classement. Le fait de stocker le classement de chaque joueur dans un jeu disposant de millions de joueurs et avec mise à jour en temps réel peut s'avérer absurdement coûteux dans une BDD relationnelle. En enlevant le traitement des relations qui n'est pas nécessaire dans ce cas, on gagne en performance.

Redis est aussi très utile en cas de messagerie instantanée pour les mêmes raisons.

## Deuxième type : colonnes larges

### SGBD le plus populaire 
Le plus populaire des systèmes de gestion de bases de donnée non-relationnelles colonnes larges est Apache Cassandra. J'utiliserai "Cassandra" et "BDD colonnes larges" de façon interchangeable.

## Pourquoi colonnes larges ?
Cette architecture est utile pour du "Big Data". Par cela, on entend des données massives arrivant à vitesses très rapides; Des données variés, tantôt structurés, tantôt sans structure; un volume très important en téraoctets et pétaoctets de données.

### "Oui" à Cassandra
Si vous comptez distribuer vos données sur des "data centers" multiples, puisque Cassandra utilise une architecture pair-à-pair lui permettant de répliquer et distribuer des données sur différents noeuds. Cassandra est adapté pour les applications critiques qui ne supportent pas du temps d'arrêt; les données sont stockés sur plusieurs noeuds dans différents "data centers", donc si jamais un "data center" tombe en panne, Cassanda n'aura pas de problèmes.


### "Non" à Cassandra
- Si vos [b]données sont fortement relationnelles[/b] et que vous voulez que vos transactions soient atomiques, cohérentes, isolées et durables (ACID), Cassandra n'est pas le bon choix. Dans MySQL, soit une transaction marche, soit elle ne marche pas. Sur Cassandra, vous pourriez tomber sur des cas où des transactions sont partiellement réussies. C'est pour cela que les systèmes dépendant de la propriété ACID ne doivent pas utiliser Cassandra. 

- Si vous vous attendez à faire beaucoup de mises à jour et de suppression de données. Cassandra est très rapide pour écrire des données massives, mais cela vient au détriment des opérations de suppression, de mise à jour et de lecture.
Pour chaque opération "UPDATE", Cassandra ne modifie pas la donnée existante, mais ajoute une nouvelle version plus récente. 
Ceci est pénalisant pour les operations le lecture qui tomberont sur des réplications de données pas très utiles.
Il s'agit de même pour les suppressions : Cassandra ne supprime pas les données mais les marque comme "mortes"; une lecture retrourera donc beaucoup de données mortes si vous supprimez beaucoup.
Eventuellement, Cassandra supprime complètement les données mortes. Mais cela arrive eventuellement, et non pas instantanément !

## Cas d'utilisation
La manière dont le modèle de données de Cassandra est organisé et le fait que Cassandra soit conçue pour des charges de travail d’écriture intensives le rendent exceptionnellement bon pour les données de capteur. Cela convient à des industries complètement différentes, que ce soit la fabrication, la logistique, la santé, l’immobilier, la production d’énergie, l’agriculture ou autre. Quels que soient les types de capteurs, Cassandra gère correctement le flux de données entrantes et offre des possibilités d'analyse plus poussée des données.

Bien que Cassandra ne fonctionne pas bien avec les transferts entre comptes bancaires et s’entend mal avec les transactions ACID, les banques peuvent toujours en bénéficier. Leurs solutions Big Data conçues pour analyser les données client peuvent fournir un niveau de sécurité supplémentaire à leurs clients en permettant la détection des fraudes. Cassandra le fait à merveille, compte tenu de sa grande vitesse et de la prise en charge de l'analyse en temps réel grâce à une intégration transparente avec Apache Spark.



