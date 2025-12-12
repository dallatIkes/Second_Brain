# Introduction

Un [[Use Case]] représente un ensemble de séquences d'actions qui sont réalisées par le système et qui produisent un résultat observable intéressant pour un acteur particulier.

Il s'agit d'identifier les fonctionnalités du système (décrit sur ce que devrait faire le système mais sans expliquer comment -> système = boîte noire)

Chaque association -> "participe à"

# Acteur

Un acteur représente un rôle joué par une entité externe (utilisateur humain, dispositif matériel ou autre système) qui interagit directement avec le système étudié

Il y a deux types d'acteurs :
- Acteurs principaux : déclencheurs des [[Use Case|cas d'utilisation]] 
- Acteurs secondaires : effectuant des tâches nécessaires à la réalisation du [[Use Case|cas d'utilisation]] à la demande du système

![[Pasted image 20241217180523.png]]

# Relation

## Association

## Héritage en acteur

![[Pasted image 20241217182831.png]]

## Héritage entre [[Use Case|cas d'utilisation]]

Généralisation des [[Use Case]]

![[Pasted image 20241217185700.png]]

## Extension 

Extension de comportement qui peut être exécuté seul

![[Pasted image 20241217192214.png]]
## Inclusion

Jamais exécuté seul, le cas source appelle obligatoirement 

![[Pasted image 20241217200421.png]]

--- 

![[Pasted image 20241217202427.png]]
