---
title: "Cryptographie post-quantique"
layout: post
post-image: "/assets/images/post_quantique/image_principale_post_quantique.jfif"
description: "Le NIST va standardiser des cryptosystèmes post-quantique début 2022. Selon les algorithmes choisis, la taille des clés (publiques et privées), la taille des chiffrés et la taille des signatures vont plus ou moins augmenter. Il va falloir s'adapter pour les incorporer aux nombreux protocoles (TLS, SSH, FTP, IKE, ...) utilisant des primitives cryptographiques asymétriques."
tags:
- 
---

source pour l'image : [https://interstices.info/petite-introduction-visuelle-a-la-cryptographie-post-quantique](https://interstices.info/petite-introduction-visuelle-a-la-cryptographie-post-quantique)

L'[algorithme quantique de Shor](https://fr.wikipedia.org/wiki/Algorithme_de_Shor) permet de factoriser efficacement un grand nombre. C'est pourquoi le cryptosystème [RSA](https://fr.wikipedia.org/wiki/Chiffrement_RSA) ne résiste pas à un ordinateur quantique de grande taille. Il existe également un algorithme quantique efficace pour le problème du logarithme discret (similaire à celui de Shor). La plupart des cryptosystèmes fondés sur des courbes elliptiques ne sont donc pas non plus résistants au quantique. Les ordinateurs quantiques d'aujourd'hui ne sont pas encore capables de réaliser ces cryptanalyses. Mais un ordinateur quantique tolérant aux fautes, disposant de quelques milliers de qubits et capables d'implémenter quelques milliards de portes quantiques rendra toute une **partie de la cryptographie actuelle obsolète**.

Quels sont les cryptosystèmes concernés ? Principalement ceux dont la sécurité est fondée sur les problèmes de factorisation et de logarithmes discrets. On trouve de tels cryptosystèmes pour assurer les 2 primitives cryptographiques suivantes :

* [Mécanisme d'encapsulation de clé](https://fr.wikipedia.org/wiki/M%C3%A9canisme_d'encapsulation_de_cl%C3%A9) (KEM).
* [Signatures numériques](https://fr.wikipedia.org/wiki/Signature_num%C3%A9rique).

En général, un cryptosystème fournissant un mécanisme d'encapsulation de clé fournit également un mécanisme d'échange de clé et un chiffrement à clé publique : ces trois primitives cryptographiques asymétriques sont très proches.

En 2016 le NIST (National Institute of Standardization) a lancé un [Appel à Propositions](https://csrc.nist.gov/CSRC/media/Projects/Post-Quantum-Cryptography/documents/call-for-proposals-final-dec-2016.pdf) pour trouver des cryptostèmes résistants au quantique et assurant ces 2 primitives cryptographiques. On dit d'un cryptosytème a priori résistant au quantique qu'il est post-quantique. En fait ces cryptosystèmes sont entièrement classiques : ils ne manipulent à aucun moment des états quantiques. Bien entendu, ces cryptosystèmes doivent également être sûrs face à d'éventuelles attaques d'ordinateur classique.

Après plusieurs tours d'évaluations et de sélections, le NIST a restreint son attention à une liste de 7 cryptosystèmes finalistes et de 8 cryptosystèmes "alternatifs". L'objectif annoncé est de **standardiser** des cryptosystèmes parmi les 7 finalistes **début 2022**. Certains cryptosystèmes parmi les alternatifs seront peut être standardisés plus tard.

## Les 7 finalistes

Les 7 finalistes sont répartis en deux catégories selon la primitive cryptographique qu'ils assurent.

**Mécanisme d'encapsulation de clé (KEM) :**

* [Classic McEliece](https://classic.mceliece.org/)
* [CRYSTALS-KYBER](https://pq-crystals.org/kyber/)
* [NTRU](https://www.ntru.org/resources.shtml)
* [SABER](https://www.esat.kuleuven.be/cosic/pqcrypto/saber/)

**Signature numérique :** 

* [CRYSTALS-DILITHIUM](https://pq-crystals.org/dilithium/index.shtml)
* [FALCON](https://falcon-sign.info/)
* [Rainbow](https://www.pqcrainbow.org/)

La sécurité de 5 de ces 7 finalistes est fondée sur la difficulté de problèmes mathématiques de réseaux _(lattices en anglais)_. Classic McEliece fait figure d'exception avec sa sécurité fondée sur un problème de code correcteur d'erreur. Rainbow, quant à lui, met à profit la difficulté d'un problème de polynômes multivariés pour assurer sa sécurité. Dans son [rapport sélectionnant les 7 finalistes](https://nvlpubs.nist.gov/nistpubs/ir/2020/NIST.IR.8309.pdf), le NIST insiste sur l'importance de conserver des cryptosystèmes fondés sur des problèmes mathématiques variés. En effet, si par exemple une avancée majeure en algorithmique met en défaut les cryptosystèmes à base de réseaux, les cryptosystèmes Classic McEliece et Rainbow seront toujours disponibles.

### 4 Mécanismes d'encapsulation de clé

#### Classic Mceliece

performances en mémoire :

<p align="center">
  <img width="650" src="/assets/images/post_quantique/space_McEliece.PNG">
</p>

source pour l'image : [https://classic.mceliece.org/nist/mceliece-20201010.pdf](https://classic.mceliece.org/nist/mceliece-20201010.pdf) section 5.2.

performances en temps :

<p align="center">
  <img width="600" src="/assets/images/post_quantique/time_McEliece.PNG">
</p>

source pour l'image : [https://classic.mceliece.org/nist/mceliece-20201010.pdf](https://classic.mceliece.org/nist/mceliece-20201010.pdf) section 5.3.

#### CRYSTALS-KYBER

Kyber-768 fournit plus de 128 bits de sécurité.

Performances pour une implémentation de référence en C (ref) et pour une implémentation optimisée en utilisant les vecteurs d'instructions AVX2 :

<p align="center">
  <img width="600" src="/assets/images/post_quantique/performances_Kyber.PNG">
</p>

source pour l'image : [https://pq-crystals.org/kyber/](https://pq-crystals.org/kyber/)

**sk** est la clé privée, **pk** est la clé publique et **ct** est le chiffré.

**gen** est l'agorithme de génération des clés, **enc** est l'algorithme de chiffrement et **dec** est l'algorithme de déchiffrement.

#### NTRU

performances :

<p align="center">
  <img width="600" src="/assets/images/post_quantique/performances_NTRU.PNG">
</p>

source pour l'image : [https://www.ntru.org/f/ntru-20190330.pdf](https://www.ntru.org/f/ntru-20190330.pdf) section 3.2

sécurité :

<p align="center">
  <img width="600" src="/assets/images/post_quantique/securite_NTRU.PNG">
</p>

source pour l'image : [https://www.ntru.org/f/ntru-20190330.pdf](https://www.ntru.org/f/ntru-20190330.pdf) section 5.3

Les catégories 1 à 5 sont définies par le NIST dans son [Appel à Propositions](https://csrc.nist.gov/CSRC/media/Projects/Post-Quantum-Cryptography/documents/call-for-proposals-final-dec-2016.pdf) dans la section 4.A.5. Chaque catégorie correspond à une sécurité au moins aussi bonne que celle d'une autre primitive cryptographique (chiffrement symétrique ou fonction de hachage). Les catégories 1, 3 et 5 en particulier font référence à différentes versions d'AES.

#### SABER

performances :

<p align="center">
  <img width="600" src="/assets/images/post_quantique/performances_SABER.PNG">
</p>

source pour l'image : [https://www.esat.kuleuven.be/cosic/pqcrypto/saber/performance.html](https://www.esat.kuleuven.be/cosic/pqcrypto/saber/performance.html)

nombre de bits de sécurité de SABER :

<p align="center">
  <img width="600" src="/assets/images/post_quantique/securite_SABER.PNG">
</p>

source pour l'image : [https://www.esat.kuleuven.be/cosic/pqcrypto/saber/](https://www.esat.kuleuven.be/cosic/pqcrypto/saber/)


#### Ordres de grandeur pour les 4 mécanismes d'encapsulation de clé

Pour les trois finalistes fondés sur des réseaux (CRYSTALS-KYBER, NTRU et SABER), les clés publiques et privées et le chiffré ont une taille de l'ordre du **kilooctet**. Les algorithmes de génération de clés, de chiffrement et de déchiffrement comptent de l'ordre d'un million de cycles (avec des différences significatives selon les crytosystèmes) pour l'implémentation de référence en C.

Pour Classic McEliece, la clé publique a une taille de l'ordre du **megaoctet** et la clé privée et le chiffré de l'ordre du kilooctet (grossièrement). Le gros défaut est la taille de la clé publique. L'utilisation de Classic McEliece sera sans doute restreinte à des cas où il est possible de conserver la clé publique assez longtemps (ce qui pose des difficultés pour assurer la [confidentialité persistante](https://fr.wikipedia.org/wiki/Confidentialit%C3%A9_persistante) : forward secracy).

### 3 signatures numériques

#### CRYSTALS-DILITHIUM

Le jeu de paramètres Dilithium3 fournit 128 bits de sécurité.

performances :

<p align="center">
  <img width="600" src="/assets/images/post_quantique/performances_Dilithium.PNG">
</p>

source pour l'image : [https://pq-crystals.org/dilithium/index.shtml](https://pq-crystals.org/dilithium/index.shtml)

#### FALCON

Falcon-512 fournit une sécurité proche de celle fournit par la signature RSA-2048 face à un ordinateur classique.

performances :
<p align="center">
  <img width="600" src="/assets/images/post_quantique/performances_Falcon.PNG">
</p>

source pour l'image : [https://falcon-sign.info/](https://falcon-sign.info/)

#### Rainbow

performances :

<p align="center">
  <img width="650" src="/assets/images/post_quantique/performances_Rainbow.PNG">
</p>

source pour l'image : [https://www.pqcrainbow.org/](https://www.pqcrainbow.org/)

Pour Rainbow (fondé sur des polynômes multivariés), les clés sont un peu plus grosses et les signatures un peu plus petites que pour les deux autres propositions de signature (fondés sur des réseaux).

### Cryptosystèmes non post-quantiques

Ce sont les cryptosystèmes asymétriques utilisés aujourd'hui.

RSA-2048 utilise un clé publique et une clé privée qui font toutes les deux quelques fois 2048 bits. En effet le module $$ n $$ fait 2048 bits mais on garde également d'autres informations dans les clés privées et publiques. Comme les facteurs $$ p $$ et $$ q $$ pour la clé privée. Ou les exposants privé ($$ d $$) et publique ($$ e $$) utilisés.

Pour les cryptosystèmes fondés sur des problèmes de courbe elliptique le nombre de bits de la clé publique est environ le double du nombre de bits de sécurité voulus. Donc une **clé publique d'environ 300 bits** fournit plus de 128 bits de sécurité.

Pour un algorithme de signature numérique, les performances et la sécurité dépendent également de la fonction de hachage utilisée et il faudrait présenter les résultats sous la forme d'un tableau à double entrée. Pour certaines signatures fondées sur des problèmes de courbe elliptique, on retrouve l'ordre de grandeur d'une clé publique dont la longueur est le double du nombre de bits de sécurité voulu. Donc une clé publique d'environ 300 bits fournit plus de 128 bits de sécurité.

## Discussion

Les clés des cryptosystèmes post-quantiques sont **globablement de plus grande taille** que celles utilisées jusqu'à présent. Il existe des différences importantes entre les différents cryptosystèmes post-quantiques.

L'enjeu à partir de 2022 et la standardisation par le NIST sera d'adapter les infrastructures qui implémentent des primitives cryptographiques de façon à ce qu'elles disposent des ressources nécessaires pour les cryptosystèmes post-quantiques. Il s'agit d'un **chantier collossal** !

Même si les ordinateurs quantiques de 2022 ne pourront sans doute pas encore implémenter l'algorithme de Shor, nous sommes dès aujourd'hui sous la menace d'une attaque en deux temps. En effet un attaquant peut enregistrer des communications chiffrées aujourd'hui et les déchiffrer à l'aide d'un ordinateur quantique dans quelques années. C'est problématique car certaines données échangées aujourd'hui seront encore sensibles dans quelques années.

De plus, dans un premier temps, on va implémenter des cryptosystèmes **hybrides** qui fournissent la sécurité d'un cryptosystème traditionnel **et** d'un cryptosystème post-quantique. En effet on souhaite éviter qu'un cryptosystème post-quantique s'avère attaquable par un ordinateur classique. Comme les cryptosystèmes post-quantiques ont moins été étudiés que les cryptosystèmes traditionnels, ce risque n'est pas négligeable. Naturellement les ressources dont un cryptostème hybride a besoin sont encore plus importantes que celles dont a besoin le cryptosystème post-quantique.

Il est donc important de réfléchir à cette **adaptation des infrastructures** à la cryptographie post-quantique **dès aujourd'hui**.
