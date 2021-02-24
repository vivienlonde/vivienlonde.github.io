---
title: "Cryptographie post-quantique"
layout: post
post-image: "/assets/images/post_quantique/"
description: ""
tags:
- 
---

L'algorithme quantique de Shor permet de factoriser efficacement un grand nombre. C'est pourquoi le cryptosystème [RSA](https://fr.wikipedia.org/wiki/Chiffrement_RSA) ne résiste pas à un ordinateur quantique de grande échelle. Il existe également un algorithme quantique efficace pour le problème du logarithme discret. La plupart des cryptosystèmes fondés sur des courbes elliptiques ne sont donc pas non plus résistants au quantique. Les ordinateurs quantiques d'aujourd'hui ne sont pas encore capable d'implémenter ces cryptanalyses. Mais un ordinateur quantique tolérants aux fautes, disposant de quelques milliers de qubits et capables d'implémenter quelques milliards de portes quantiques rendra toute une partie de la cryptographie actuelle obsolète.

Quelles sont les cryptosystèmes concernés ? Principalement ceux dont la sécurité est fondée sur les problèmes de factorisation et de logarithmes discrets. On trouve de tels cryptosystèmes pour assurer les 2 primitives cryptographiques suivantes :

* [Mécanisme d'encapsulation de clé](https://fr.wikipedia.org/wiki/M%C3%A9canisme_d'encapsulation_de_cl%C3%A9) (KEM).
* [Signatures numériques](https://fr.wikipedia.org/wiki/Signature_num%C3%A9rique).

En général, un cryptosystème fournissant un mécanisme d'encapsulation de clé fournit également un mécanisme d'échange de clé et un chiffrement à clé publique : ces trois primitives cryptographiques sont proches.

En 2016 le NIST (National Institute of Standardization) a lancé un appel à propositions pour trouver des cryptostèmes résistants au quantique et assurant ces 2 primitives cryptographiques. On dit d'un cryptosytème a priori résistant au quantique qu'il est post-quantique. Ces cryptosystèmes sont entièrement classiques : ils ne manipulent à aucun moment ces états quantiques. On utilise le qualificatif post-quantique uniquement pour signifier qu'un ordinateur quantique de grande taille ne semble pas mettre en danger la sécurité de ces cryptosystèmes. Bien entendu, ces cryptosystèmes doivent également être sûrs face à d'éventuelles attaques d'ordianteur classique.

Après plusieurs tours d'évaluations et de sélections, le NIST a restreint son attention à une liste de 7 cryptosystèmes finalistes et de 8 cryptosystèmes "alternatifs". L'objectif annoncé est de standardiser des cryptosystèmes parmi les 7 finalistes début 2022. Certains cryptosystèmes parmi les alternatifs seront peut être standardisés plus tard.

## Les 7 finalistes

Les primitives de chiffrement à clé publique et d'échange de clé sont très proches et un même cryptosystème peut généralement assurer les deux fonctions. Les 7 finalistes sont répartis en deux catégories selon la primitive cryptographique qu'ils assurent.

**Chiffrement à clé publique et échange de clés :**

* [Classic McEliece](https://classic.mceliece.org/)
* [CRYSTALS-KYBER](https://pq-crystals.org/kyber/)
* [NTRU](https://www.ntru.org/resources.shtml)
* [SABER](https://www.esat.kuleuven.be/cosic/pqcrypto/saber/)

**Signature numérique :** 

* [CRYSTALS-DILITHIUM](https://pq-crystals.org/dilithium/index.shtml)
* [FALCON](https://falcon-sign.info/)
* [Rainbow](https://www.pqcrainbow.org/)

La sécurité de 5 de ces 7 finalistes est fondée sur la famille de problèmes mathématiques de réseaux _(lattices en anglais)_. Classic McEliece fait figure d'exception avec sa sécurité fondée sur un problème de code correcteur d'erreur. Rainbow, quant à lui, met à profit la difficulté d'un problème de polynômes multivariés pour assurer sa sécurité. Dans son [rapport](https://nvlpubs.nist.gov/nistpubs/ir/2020/NIST.IR.8309.pdf), le NIST insiste sur l'importance de conserver des cryptosystèmes fondés sur des problèmes mathématiques variés. En effet, si par exemple une avancée majeure en algorithmique met en défaut les cryptosystèmes à base de réseaux, les cryptosystèmes Classic McEliece et Rainbow seront toujours disponibles.

### 4 Mécanismes d'encapsulation de clé

#### Classic Mceliece

la clé publique a une taille de l'ordre du megaoctet et la clé privée de l'ordre du kilooctet. Qu'en est est-il du chiffré (kilooctet je crois) et des algorithmes (efficaces je crois) ?

#### CRYSTALS-KYBER

Kyber-768 fournit plus de 128 bits de sécurité.

Performances pour une implémentation de référence en C (ref) et pour une implémentation optimisée en utilisant les vecteurs d'instructions AVX2 :

<p align="center">
  <img width="600" src="/assets/images/post_quantique/performances_Kyber.PNG">
</p>

source pour l'image : [https://pq-crystals.org/kyber/](https://pq-crystals.org/kyber/)

**sk** est la clé privée, **pk** est la clé publique et **ct** est le chiffré. **gen** est l'agorithme de génération des clés, **enc** est l'algorithme de chiffrement et **dec** est l'algorithme de déchiffrement.

#### NTRU

<p align="center">
  <img width="600" src="/assets/images/post_quantique/performances_NTRU.PNG">
</p>

source pour l'image : [https://www.ntru.org/f/ntru-20190330.pdf](https://www.ntru.org/f/ntru-20190330.pdf) section 3.2

<p align="center">
  <img width="600" src="/assets/images/post_quantique/securite_NTRU.PNG">
</p>

source pour l'image : [https://www.ntru.org/f/ntru-20190330.pdf](https://www.ntru.org/f/ntru-20190330.pdf) section 5.3

#### SABER

nombre de bits de sécurité de SABER :

<p align="center">
  <img width="600" src="/assets/images/post_quantique/securite_SABER.PNG">
</p>

source pour l'image : [https://www.esat.kuleuven.be/cosic/pqcrypto/saber/](https://www.esat.kuleuven.be/cosic/pqcrypto/saber/)

performances :

<p align="center">
  <img width="600" src="/assets/images/post_quantique/performances_SABER.PNG">
</p>

source pour l'image : [https://www.esat.kuleuven.be/cosic/pqcrypto/saber/performance.html](https://www.esat.kuleuven.be/cosic/pqcrypto/saber/performance.html)

#### Ordres de grandeur pour les 4 mécanismes d'encapsulation de clé

Pour CRYSTALS-KYBER, NTRU et SABER, les clés publiques et privées et le chiffré ont une taille de l'ordre du kilooctet. Les algorithmes de génération de clés, de chiffrement et de déchiffrement comptent de l'ordre d'un million de cycles (avec des différences significatives selon les crytosystèmes) pour l'implémentation de référence en C.

Pour Classic McEliece, la clé publique a une taille de l'ordre du megaoctet et la clé privée de l'ordre du kilooctet. Qu'en est est-il du chiffré (kilooctet je crois) et des algorithmes (efficaces je crois) ? Le gros défaut est la taille de la clé publique.

### 3 signatures numériques

#### CRYSTALS-DILITHIUM

Le jeu de paramètres Dilithium3 fournit 128 bits de sécurité.

<p align="center">
  <img width="600" src="/assets/images/post_quantique/performances_Dilithium.PNG">
</p>

source pour l'image : [https://pq-crystals.org/dilithium/index.shtml](https://pq-crystals.org/dilithium/index.shtml)

#### FALCON

Falcon-512 fournit une sécurité proche de celle fournit par RSA-2048 face à un ordinateur classique.

performances :
<p align="center">
  <img width="600" src="/assets/images/post_quantique/performances_Falcon.PNG">
</p>

source pour l'image : [https://falcon-sign.info/](https://falcon-sign.info/)

#### Rainbow

<p align="center">
  <img width="600" src="/assets/images/post_quantique/performances_Rainbow.PNG">
</p>

source pour l'image : [https://www.pqcrainbow.org/](https://www.pqcrainbow.org/)

Pour Rainbow, les clés sont un peu plus grosses mais les signatures sont un peu plus petites.

## Cryptosystèmes non post-quantiques

RSA-2048 utilise un clé publique de 2048 bits. La clé privée est très petite.
Pour les cryptosystèmes à base de courbe elliptique le nombre de bits de la clé publique est environ le double du nombre de bits de sécurité voulus. Donc une clé publique de 300 bits fournit plus de 128 bits de sécurité.

Pour un algorithme de signature, les performances dépendent également de la fonction de hachage utilisée.