---
title: Calcul quantique - la technique du retour de phase
layout: post
post-image: "https://raw.githubusercontent.com/thedevslot/WhatATheme/master/assets/images/SamplePost.png?token=AHMQUEPC4IFADOF5VG4QVN26Z64GG"
description: A sample post to show how the content will look and how will different
  headlines, quotes and codes will be represented.
tags:
- sample
- post
- test
---

Le retour de phase (en anglais phase kickback) est le point fondamental de l'algorithme d'estimation quantique de phase. On retrouve également cette technique sous des formes dérivées dans les algorithmes quantiques suivant:
* Deutsch-Jozsa
* Shor
* …

Sous sa forme élémentaire, le retour de phase correspond au circuit suivant:

AJOUTER CIRCUIT

On suppose que l'état $$ | \psi \rangle $$ est un état propre de la matrice unitaire $$ U $$. C'est pourquoi lorsqu'on applique $$ U $$ à l'état $$ | \psi \rangle $$, il acquiert une phase $$ \phi $$. L'état $$ | \psi \rangle $$ peut être constitué d'un ou de plusieurs qubits. En revanche la ligne du haut correspond à un seul qubit, qu'on va appeler le qubit de contrôle.  Comme la matrice $$ U $$ est appliquée uniquement lorsque le qubit de contrôle est dans l'état $$ | 1 \rangle $$, seule cette partie de la superposition acquiert la phase $$ \phi $$. Finalement l'état $$ | \psi \rangle $$ n'est pas modifié. Il peut donc être réutilisé. En revanche le qubit de contrôle a enregistré une propriété de l'état $$ | \psi \rangle $$ et de la matrice $$ U $$. Après un éventuel post-traitement, on peut mesurer le qubit de contrôle pour obtenir de l'information sur $$ \phi $$.
Toutes les variantes de l'estimation quantique de phase utilisent le retour de phase comme primitive. Selon les itérées de $$ U $$ qui sont appliquées ($$ U^2 $$, $$ U^3 $$, …) et selon le post-traitement du ou des qubits de contrôle, l'algorithme s'appellera l'estimation quantique de phase de Kitaev, l'estimation quantique de phase itérative, l'estimation quantique de phase robuste ou encore l'estimation quantique de phase avec marche aléatoire.

# Fonction booléenne et retour de phase

La technique du retour de phase n'est pas seulement utile pour l'estimation quantique de phase. Le retour de phase permet également de transformer une opération quantique qui enregistre le résultat d'une fonction booléenne dans un qubit auxiliaire en une opération quantique qui enregistre ce résultat dans la phase de chaque état quantique.

On considère une fonction booléenne qui prend $$n$$ bits en entrée et en renvoie $$1$$ en sorie $$ f : \{0, 1\}^n \rightarrow \{0, 1\} $$. Comme une opération quantique doit toujours être réversible (AJOUTER LIEN) on implémente généralement ce type d'opération en laissant les $$n$$ qubits d'input inchangés et en utilisant un qubit supplémentaire (dit qubit auxiliaire) pour enregistrer le résultat de la fonction. $$ U_f $$ est l'opération quantique qui correspond à la fonction $$ f $$:

<p align="center">
$$ U_f (|x\rangle |0\rangle) = |x\rangle |f(x)\rangle $$
</p>


Parfois il est préférable d'enregistrer le résultat de la fonction $$ f $$ sans utiliser de qubit auxiliaire. En enregistrant ce résultat directement dans la phase de chaque état quantique, on assure que l'opération quantique $$ \tilde{U}_f $$ soit réversible: