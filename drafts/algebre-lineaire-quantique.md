---
title: "Algèbre linéaire quantique"
layout: post
post-image: "/assets/images/algebre_lineaire_quantique/?"
description: ""
tags:
- Input et output
- Encodage par projecteurs
- transformation de valeurs singulières
---

Une technique majeure permettant de réaliser des opérations d'algèbre linéaire à l'aide d'un ordinateur quantique est l'encodage par projecteurs (en anglais projectors encoding). En effet de nombreuses autres techniques d'encodage peuvent être vues comme un cas particulier de cette méthode :

- les oracles pour matrices creuses.
- les combinaisons linéaires de matrices unitaires.
- les encodages de matrices de transition et de chaînes de Markov.

On dit qu'une matrice $$ A $$ est encodée par projecteurs s'il existe une unitaire $$ U $$ et deux projecteurs orthogonaux $$ \Pi $$ et $$ \tilde{\Pi} $$ tels que :

$$ A = \tilde{\Pi} U \Pi $$

Concrètement, en termes de calcul quantique :

- $$ U $$ est la matrice unitaire qu'on peut implémenter sur un ordinateur quantique à l'aide d'une succession de portes quantiques.
- $$ \Pi $$ décrit l'ensemble des états quantiques initiaux auxquels on s'intéresse. Plus précisément, on ne considère pas les états quantiques qui n'appartiennent pas à $$ \text{Im}(\Pi) $$. On suppose implicitement qu'on n'appliquera jamais $$ U $$ à ces états. Ou plutôt on ne donne aucune garantie sur les résultats qu'on obtiendrait si on appliquait $$ U $$ à un état quantique qui n'appartient pas à $$ \text{Im}(\Pi) $$.
- $$ \tilde{\Pi} $$ décrit l'ensemble des états quantiques finaux auxquels on s'intéresse. Plus précisément, lorsqu'on réalise une mesure quantique correspondant au projecteur $$ \tilde{\Pi} $$, on peut obtenir deux résultats : $$ 1 $$ pour un état quantique appartenant à l'image de $$ \tilde{\Pi} $$ et $$ 0 $$ pour un état quantique appartenant au noyau de $$ \tilde{\Pi} $$. Si après avoir appliqué $$ U $$, on réalise la mesure quantique correspondant à $$ \tilde{\Pi} $$ et on obtient $$ 0 $$, on ne peut rien dire sur l'état quantique associé. En revanche si le résulat de cette mesure donne $$ 1 $$ et que l'état quantique initial était licite (c'est-à-dire appartenait à $$ \text{Im}(\Pi) $$), alors l'état quantique obtenue après la mesure est égal à l'état quantique initial auquel on a appliqué la matrice $$ A $$.

L'utilisation des projecteurs orthogonaux $$ \Pi $$ et $$ \tilde{\Pi} $$ met en lumière les rôles symétriques joués en mécanique quantique par la préparation d'état et la mesure. On parle ici de préparation selon le projecteur $$ \Pi $$ et de post-sélection selon le projecteur $$ \tilde{\Pi} $$. Lorsque ces deux conditions sont satisfaites l'unitaire $$ U $$ implémente la matrice $$ A $$.

## Normalisation de la matrice A

En tant que bloc d'une matrice unitaire, la matrice $$ A $$ doit avoir toutes ses valeurs propres inférieures à 1 en norme. Si ce n'est pas le cas on peut trouver un encodage par projecteurs d'un multiple de $$ A $$.

Lorsqu'on réalise la mesure correspondant à $$ \tilde{\Pi} $$ et qu'on obtient $$ 1 $$, on renormalise la projection de l'état quantique $$ A \vert \psi_{initial} \rangle $$. La probabilité de succès de l'algorithme peut donc dépendre de $$ \vert \psi_{initial} \rangle $$. Plus exactement la probabilité de succès est égale à $$ \vert \tilde{\Pi} A \vert \psi_{initial} \rangle \vert^2 $$.

Une façon alternative de comprendre le rôle de $$ \tilde{\Pi} $$ est de considérer qu'on termine l'algorithme quantique par une mesure totale selon une base adaptée à $$ \tilde{\Pi} $$. C'est-à-dire que chaque élément de cette base appartient ou bien à l'image de $$ \tilde{\Pi} $$ ou bien à son noyau. Si la mesure donne un résultat correspondant au noyau de $$ \tilde{\Pi} $$, on considère que le calcul quantique a échoué. On n'obtient aucune information dans ce cas. Si au contraire on obtient un résultat correspond à l'image de $$ \tilde{\Pi} $$, le calcul quantique a réussi. Le résultat de la mesure est un tirage parmi tous les éléments de la base correspondant à l'image de $$ \tilde{\Pi} $$ selon la distribution de probabilité correspondant à $$ A \vert \psi_{initial} \rangle $$. Dans ce cas on obtient donc de l'information sur $$ A $$.

La plupart des algorithmes quantiques consistent à utiliser $$ U $$, $$ \Pi $$, $$ \tilde{\Pi} $$ comme des briques élémentaires permettant d'implémenter des transformations de $$ A $$. C'est-à-dire que $$ A $$ et sa représentation par le triplet $$ (U, \Pi, \tilde{\Pi}) $$ sont des paramètres de l'algorithme quantique. La travail consistant pour un $$ A $$ donné à trouver une telle représentation et une façon efficace de décomposer $$ U $$ en portes à un ou deux qubits n'est pas encore fait : il est laissé à ceux qui trouveront des applications utiles à cet algorithme quantique.

De plus le résultat d'un tel algorithme quantique est un état quantique dont la projection selon $$ \tilde{\Pi} $$ donne un état quantique encodant une distribution de probabilité intéressante. Si on veut reconstituer cette distribution de probabilité, il va falloir mesurer l'état quantique final et répéter l'algorithme quantique de nombreuses fois pour obtenir suffisamment de statistiques.  
Les cas favorables sont ceux où la distribution de probabilité intéressante porte sur un faible nombre d'état : il est alors plus rapide d'échantillonner cette distribution de probabilité.

Ces deux problèmes des algorithmes quantiques peuvent être désignés de façon succinte par l'expression "problèmes d'input et d'output" des algorithmes quantiques. Voici une liste des algorithmes appartenant à cette catégorie :

- Inversion d'une matrice.
- Marches quantiques.

Voici une liste d'algorithmes utilisant ce type de techniques mais ayant résolu le problème d'output :

- amplification d'amplitude et ses variantes (à point fixe, robuste et oblivious, ...) lorsque le but est de trouver un état marqué.

La simulation moléculaire résout le problème d'output en extrayant une énergie par estimation de phase. Cela demande tout de même de répéter l'algorithme de l'ordre de $$ \frac{1}{\epsilon} $$ fois pour une précision $$ \epsilon $$. Elle adresse le problème d'input par encodage (Jordan-Wigner ou Bravyi-Kitaev) et en partie par l'expression d'un Hamiltonien comme une somme de termes plus faciles à implémenter.

La régression en composantes principales amortit le problème d'input. Je ne sais pas si le problème d'output est géré. (à creuser).

Il n'y a pas de problème d'output lorsque la complexité du calcul est nettement supérieure au nombre d'échantillons nécessaires pour obtenir des statistiques satisfaisantes.

La transformation des vecteurs singuliers à droite en vecteurs singuliers à gauche ne parle ni des problèmes d'input ni des problèmes d'output.

La résolution de problèmes d'optimisation convexes ne résout pas le problème d'output (à ma connaissance). En effet des systèmes linéaires sont résolus en suivant la méthode du simplexe. Il faudrait comprendre s'il est nécessaire d'avoir une description classique des solutions de ces systèmes linéaires. Il faudrait aussi regarder comment fonctionne la méthode quantique du point intérieur de I. Kerenidis.

Dans les cas de l'inversion de matrice et de la simulation moléculaire, l'avantage exponentielle vient de la taille de l'espace de modélisation quantique (exponentielle en le nombre de qubits). Il est étonnant qu'il n'existe pas d'algorithmes stochastiques pour ces problèmes proposant également une réduction exponentielle de la mémoire nécessaire.

Les algorithmes quantiques de Monte Carlo (i.e. estimation de probabilité), permettant par exemple le pricing de produits dérivés, résolvent le problème de l'output par estimation d'amplitude. Cela demande tout de même de répéter l'algorithme de l'ordre de $$ \frac{1}{\epsilon} $$ fois pour une précision $$ \epsilon $$.
