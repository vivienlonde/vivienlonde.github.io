---
title: Calcul quantique - la technique du retour de phase
layout: post
post-image: "/assets/images/retour_de_flamme.jpg"
description: A sample post to show how the content will look and how will different
  headlines, quotes and codes will be represented.
tags:
- sample
- post
- test
---

Le retour de phase (en anglais phase kickback) est le point fondamental des algorithmes quantiques d'estimation de phase. On retrouve également cette technique sous des formes dérivées dans les algorithmes quantiques suivant:
* Deutsch-Jozsa
* Shor
* …

## Retour de phase et les algorithmes d'estimation de phase

Sous sa forme élémentaire, le retour de phase correspond au circuit suivant:

<p align="center">
  <img width="460" height="300" src="/assets/images/phase_kickback.PNG">
</p>

On a supposé ici que l'état $$ \vert \psi \rangle $$ est un état propre de la porte $$ U $$. C'est à dire que lorsqu'on applique $$ U $$ à l'état $$ \vert \psi \rangle $$, il acquiert une phase $$ \phi $$:

<p align="center">
$$ U \vert \psi \rangle = e^{i\phi} \vert \psi \rangle $$
</p>

L'état $$ \vert \psi \rangle $$ peut être constitué d'un ou de plusieurs qubits. En revanche la ligne du haut correspond à un seul qubit, qu'on va appeler le qubit de contrôle.  Comme la matrice $$ U $$ est appliquée uniquement lorsque le qubit de contrôle est dans l'état $$ \vert 1 \rangle $$, seule cette partie de la superposition acquiert la phase $$ \phi $$. Finalement **l'état $$ \vert \psi \rangle $$ n'est pas modifié**. Il peut donc être réutilisé. En revanche **le qubit de contrôle a enregistré de l'information sur $$ \phi $$**, c'est-à-dire sur une propriété de l'état $$ \vert \psi \rangle $$ et de la matrice $$ U $$. Ce résultat est très contre-intuitif car on pourrait penser naïvement que l'état du qubit de contrôle ne sera pas modifié et que l'état $$ \psi $$ sera modifié lorsque le qubit de contrôle est dans l'état $$ \vert 1 \rangle $$. Par ailleurs ce résultat est très utile car la ressource précieuse (l'état $$ \psi $$) n'est ni mesurée ni modifiée par ce circuit.

Après un éventuel post-traitement, on peut mesurer le qubit de contrôle pour obtenir de l'information sur $$ \phi $$. Un circuit très simple qui permet de récupérer de l'information sur $$ \phi $$ est le suivant:

<p align="center">
  <img width="460" height="300" src="/assets/images/elementary_phase_estimation.PNG">
</p>

Lorsqu'on réalise ce circuit quantique, le résultat de la mesure du qubit de contrôle est $$ 0 $$ avec probabilité $$ \cos^2(\frac{\phi}{2}) $$ et $$ 1 $$ avec probabilité $$ \sin^2(\frac{\phi}{2}) $$. Chaque exécution de ce circuit quantique apporte donc un peu d'information sur $$ \phi $$.

Toutes les variantes de l'estimation de phase utilisent le retour de phase comme primitive. Selon les itérées de $$ U $$ qui sont appliquées ($$ U^2 $$, $$ U^3 $$, …) et selon le post-traitement du ou des qubits de contrôle, l'algorithme s'appellera l'[estimation quantique de phase](https://en.wikipedia.org/wiki/Quantum_phase_estimation_algorithm) ou l'une des différentes variantes de l'[estimation itérative de phase](https://docs.microsoft.com/en-us/quantum/user-guide/libraries/standard/characterization#iterative-phase-estimation) :

* l'estimation bayésienne de phase.
* l'estimation robuste de phase.
* l'estimation par marche aléatoire de phase.

## Fonction booléenne et retour de phase

La technique du retour de phase n'est pas seulement utile pour l'estimation quantique de phase. Le retour de phase permet également de transformer une opération quantique qui enregistre le résultat d'une fonction booléenne dans un qubit auxiliaire en une opération quantique qui enregistre ce résultat dans la phase de chaque état quantique.

On considère une fonction booléenne qui prend $$n$$ bits en entrée et en renvoie $$1$$ en sortie $$ f : \{0, 1\}^n \rightarrow \{0, 1\} $$. Comme une opération quantique doit toujours être réversible (AJOUTER LIEN) on implémente généralement ce type d'opération en laissant les $$n$$ qubits d'input inchangés et en utilisant un qubit supplémentaire (dit qubit auxiliaire) pour enregistrer le résultat de la fonction. $$ U_f $$ est l'opération quantique qui correspond à la fonction $$ f $$:

<p align="center">
$$ U_f ( \, \vert x \rangle \vert 0 \rangle \, ) = \vert x \rangle \vert f(x) \rangle $$
</p>

Parfois il est préférable d'enregistrer le résultat de la fonction $$ f $$ sans utiliser de qubit auxiliaire. En enregistrant ce résultat directement dans la phase de chaque état quantique, on assure que l'opération quantique $$ \tilde{U}_f $$ soit réversible:

<p align="center">
$$ \tilde{U}_f ( \, \vert x \rangle \, ) = (-1)^{f(x)} \vert f(x) \rangle $$
</p>

Il est souvent plus facile d'implémenter l'opération quantique $$ U_f $$, qu'on appellera désormais **l'oracle à qubit auxiliaire**. En effet on peut sans grande difficulté adapter le circuit classique qui permet de calculer $$ f $$ pour obtenir le circuit quantique qui permet de calculer $$ U_f $$. En revanche dans de nombreux algorithmes quantiques comme par exemple l'algorithme de Grover (AJOUTER LIEN) et l'algorithme de Deutsch-Jozsa (AJOUTER LIEN), on a besoin de l'opération quantique $$ \tilde{U}_f $$, qu'on appellera désormais **l'oracle à phase**.

Heureusement la technique du retour de phase permet de transformer un oracle à qubit auxiliaire en un oracle à phase:

1. On applique une porte $$ X $$ (AJOUTER LIEN) puis une porte de Hadamard (AJOUTER LIEN) au qubit auxiliaire.
2. On applique l'oracle à qubit auxiliaire au système constitué des qubits d'input et du qubit auxiliaire.
3. On applique une porte de Hadamard puis une porte $$ X $$ au qubit auxiliaire.

Vérifions qu'on obtient bien la transformation attendue pour chaque état \\( \vert x \rangle \\) des qubits d'input.

Les portes X et de Hadamard permettent de mettre le qubit auxiliaire dans l'état $$ \frac{1}{\sqrt{2}} ( \vert 0 \rangle - \vert 1 \rangle) $$.

#### 1er cas : f(x)=0

L'oracle à qubit n'a aucun effet dans ce cas.

La porte de Hadamard et la porte $$ X $$ remettent le qubit auxiliaire dans l'état $$ \vert 0 \rangle $$.

#### 2eme cas : f(x)=1

L'oracle à qubit auxiliaire change la partie $$ \vert 0 \rangle $$ du qubit auxiliaire en $$ \vert 1 \rangle $$ et sa partie $$ \vert 1 \rangle $$ en $$ \vert 0 \rangle $$. Ainsi après application de l'oracle à qubit auxiliaire, le qubit auxiliaire est dans l'état:

<p align="center">
$$ \frac{1}{\sqrt{2}} ( \vert 1 \rangle - \vert 0 \rangle) = - \frac{1}{\sqrt{2}} ( \vert 0 \rangle - \vert 1 \rangle) $$
</p>

Comme la phase est une propriété globale du système, on peut considérer que le qubit auxiliaire est dans l'état $$ \frac{1}{\sqrt{2}} ( \vert 0 \rangle - \vert 1 \rangle) $$ et que les qubits d'input sont dans l'état $$ - \vert x \rangle $$.

La porte de Hadamard et la porte $$ X $$ remmettent finalement le qubit auxiliaire dans l'état $$ \vert 0 \rangle $$.

#### Bilan

On voit que dans les deux cas, le qubit auxiliaire reste dans son état de départ ($$ \vert 0 \rangle $$) et le registre d'input est transformé de l'état $$ \vert x \rangle $$ à l'état $$ (-1)^{f(x)} \vert x \rangle $$. On a donc réussi à construire un **oracle à phase** à partir d'un **oracle à qubit auxiliaire**.

## Lien avec la technique du retour de phase

L'état $$ \vert - \rangle = \frac{1}{\sqrt{2}} ( \vert 0 \rangle - \vert 1 \rangle) $$ est un état propre de la porte $$ X $$ avec valeur propre $$ -1 $$:

<p align="center">
$$ X \vert - \rangle = - \vert - \rangle. $$
</p>

De plus appliquer un oracle à qubit auxiliaire revient à appliquer une porte $$ X $$ au qubit auxiliaire en contrôlant sur les états $$ \vert x \rangle $$ tels que $$ f(x)=1 $$. Par retour de phase, seuls les états $$ \vert x \rangle $$ tels que $$ f(x)=1 $$ vont acquérir la valeur propre de l'état $$ \vert - \rangle $$ pour la porte $$ X $$, à savoir la phase -1.

La transformation d'un oracle à qubit auxiliaire en un oracle à phase fournit donc un deuxième cas d'utilisation de la technique du retour de phase. Dans ce cas les qubits d'input acquièrent de l'information et le qubit auxiliaire joue le rôle de l'état propre $$ \vert \psi \rangle $$. A l'inverse dans le cas de l'estimation de phase, le qubit auxiliaire acquière de l'information et l'état propre $$ \vert \psi \rangle $$ est laissé inchangé.