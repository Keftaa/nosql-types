
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

