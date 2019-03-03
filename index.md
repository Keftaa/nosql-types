
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

### Pourquoi colonnes larges ?
Cette architecture est utile pour du "Big Data". Par cela, on entend des données massives arrivant à vitesses très rapides; Des données variés, tantôt structurés, tantôt sans structure; un volume très important en téraoctets et pétaoctets de données.

#### "Oui" à Cassandra
Si vous comptez distribuer vos données sur des "data centers" multiples, puisque Cassandra utilise une architecture pair-à-pair lui permettant de répliquer et distribuer des données sur différents noeuds. Cassandra est adapté pour les applications critiques qui ne supportent pas du temps d'arrêt; les données sont stockés sur plusieurs noeuds dans différents "data centers", donc si jamais un "data center" tombe en panne, Cassanda n'aura pas de problèmes.


#### "Non" à Cassandra
- Si vos [b]données sont fortement relationnelles[/b] et que vous voulez que vos transactions soient atomiques, cohérentes, isolées et durables (ACID), Cassandra n'est pas le bon choix. Dans MySQL, soit une transaction marche, soit elle ne marche pas. Sur Cassandra, vous pourriez tomber sur des cas où des transactions sont partiellement réussies. C'est pour cela que les systèmes dépendant de la propriété ACID ne doivent pas utiliser Cassandra. 

- Si vous vous attendez à faire beaucoup de mises à jour et de suppression de données. Cassandra est très rapide pour écrire des données massives, mais cela vient au détriment des opérations de suppression, de mise à jour et de lecture.
Pour chaque opération "UPDATE", Cassandra ne modifie pas la donnée existante, mais ajoute une nouvelle version plus récente. 
Ceci est pénalisant pour les operations le lecture qui tomberont sur des réplications de données pas très utiles.
Il s'agit de même pour les suppressions : Cassandra ne supprime pas les données mais les marque comme "mortes"; une lecture retrourera donc beaucoup de données mortes si vous supprimez beaucoup.
Eventuellement, Cassandra supprime complètement les données mortes. Mais cela arrive eventuellement, et non pas instantanément !

### Cas d'utilisation
La manière dont le modèle de données de Cassandra est organisé et le fait que Cassandra soit conçue pour des charges de travail d’écriture intensives le rendent exceptionnellement bon pour les données de capteur. Cela convient à des industries complètement différentes, que ce soit la fabrication, la logistique, la santé, l’immobilier, la production d’énergie, l’agriculture ou autre. Quels que soient les types de capteurs, Cassandra gère correctement le flux de données entrantes et offre des possibilités d'analyse plus poussée des données.

Bien que Cassandra ne fonctionne pas bien avec les transferts entre comptes bancaires et s’entend mal avec les transactions ACID, les banques peuvent toujours en bénéficier. Leurs solutions Big Data conçues pour analyser les données client peuvent fournir un niveau de sécurité supplémentaire à leurs clients en permettant la détection des fraudes. Cassandra le fait à merveille, compte tenu de sa grande vitesse et de la prise en charge de l'analyse en temps réel grâce à une intégration transparente avec Apache Spark.

## Troisième type : documents

### SGBD le plus populaire
Le plus populaire des systèmes de gestion de bases de données non-relationnelles en document est MongoDB. J'utiliserai "MongoDB" et "BDD document" de façon interchangeable.

### Pourquoi BDD document ?
Les bases de données "document store" sont similaires aux BDD clé-valeur dans le fait qu'elles contiennent une clé et une valeur. En effet, les données sont stockées comme des valeurs, et leur clé est l'indentificateur unique pour cette valeur.
La différence est que la valeur peut contenir des données structurées ou semi-structurée (alors que dans une BDD clé-valeur la valeur est un "blob" dont la BDD ne prend pas compte de la structure). 


### Cas d'utilisation
Il y a une raison pour appeler MongoDB de "base de données de documents" parce que c'est vraiment pour stocker des données uniques et fonctionne bien pour des tâches telles que l'archivage de données, la création de rapports de données et les données dynamiques qui ne peuvent pas être contraintes dans un schéma prédéfini. Imaginez un site e-commerce où les vendeurs peuvent ajouter des produits à vendree. Ces produits peuvent avoir différentes propriétés. Dans ce cas, la nature semi-structurée de MongoDB rendra le travail plus facile que dans une base de données traditionnelle. 


## Quatrième type : BDD graphiques

### SGBD le plus populaire
Neo4J. 

### Pourquoi BDD graphiques ?
- Les bases de données graphiques reposent essentiellement sur le modèle Entité - Attribut - Valeur. 
- Les entités sont également appelées nœuds, qui ont des propriétés. C'est un moyen très flexible de décrire le lien entre les données et d'autres données:  
1. Les nœuds stockent des données sur chaque entité de la base de données. 
2. Les relations décrivent une relation entre les nœuds et une propriété est simplement le nœud situé à l'extrémité opposée de la relation. 

Alors qu'une base de données traditionnelle stocke une description de chaque relation possible dans des champs de clé étrangère ou des tables de jonctions, les bases de données graphiques permettent de définir pratiquement n'importe quelle relation à la volée.

#### Et pourquoi pas ?
Les BDD en graphe sont indexés par relation. Donc, ce type est performant quand votre modèle nécessite la traversée de beaucoup de relations. Par contre, ceci vient au détriment de la gestion de données par listes. C'est à dire que quand votre modèle est plutôt analytique ou quand il plus sur la séquence de données que sur la relation entre les données, Neo4J et cie ne sont pas les meilleurs.

### Cas d'utilisation
Les graphes sont une méthode très naturelle pour modéliser certaines sources de données (mais pas toutes), telles que les réseaux poste à poste, les cartes routières, les structures organisationnelles, les réseaux sociaux etc.


