---
title: "Composition de réflexions"
layout: post
post-image: "/assets/images/reflexions/?"
description: ""
tags:
- Amplification d'Amplitude
- Marches Quantiques
---

## Grover avec un seul état marqué

On considère un système quantique constitué de $$ n $$ qubits. L'un des état de la base computationnelle est marqué. On le note $$ \vert m \rangle $$. L'état de superposition uniforme est défini ainsi : $$ \vert s \rangle := \frac{1}{\sqrt{2^n}} \sum_{i=0}^{2^n} \vert i \rangle $$. On considère les réflexions par rapport à ces deux états:

$$ R_m = I - 2 \vert m \rangle \langle m \vert, $$

$$ R_s = I - 2 \vert s \rangle \langle s \vert. $$

Nous allons étudier en détails dans ce billet de blog l'opérateur de Grover: $$ U_g := R_m R_s $$.

$$ U_g = I - 2 \vert s \rangle \langle s \vert - 2 \vert m \rangle \langle m \vert + 4 \langle s \vert m \rangle \vert s \rangle \langle m \vert. $$

On peut se restreindre au sous-espace vectoriel $$ F := \text{Vect} ( \vert m \rangle, \vert s \rangle) $$ car $$ U_g $$ agit comme l'identité sur un supplémentaire orthogonal de $$ F $$. Attention au fait que les vecteurs $$ \vert m \rangle $$ et $$ \vert s \rangle $$ ne sont pas orthogonaux. On note dorénavant $$ \alpha := \langle s \vert m \rangle $$. Remarquez que $$ \langle m \vert s \rangle = \bar{\alpha} $$ par définition d'un produit Hermitien.

$$ \begin{align*}
U_g \vert m \rangle &= \vert m \rangle - 2 \alpha \vert s \rangle -2 \vert m \rangle + 4 \alpha \vert s \rangle \\
                    &= - \vert m \rangle + 2 \alpha \vert s \rangle
\end{align*} $$

$$ \begin{align*}
U_g \vert s \rangle &= \vert s \rangle - 2 \vert s \rangle -2 \bar{\alpha} \vert m \rangle + 4 \vert \alpha \vert^2 \vert s \rangle \\
                    &= (4 \vert \alpha \vert^2 - 1) \vert s \rangle - 2 \bar{\alpha} \vert m \rangle
\end{align*} $$

La matrice de $$ U_g $$ dans la base (non orthogonale) $$( \vert m \rangle, \vert s \rangle)$$ est donc :

$$ M_g := \begin{pmatrix}
-1 & - 2 \bar{\alpha}  \\
2 \alpha & 4 \vert \alpha \vert^2 - 1
\end{pmatrix} $$

On peut vérifier facilement que le déterminant de $$ M_g $$ vaut $$ 1 $$. (On le savait déjà puisque $$ \det R_m = -1 $$ et $$ \det R_s = -1 $$). On note $$ \chi $$ le polynome charactéristique de $$ M_g $$ :

$$ \chi = X^2 + 2 (2 \vert \alpha \vert^2 - 1) X + 1. $$

Comme $$ 0 < \vert \alpha \vert^2 < 1 $$, on peut définir $$ \theta := \arccos (2 \vert \alpha \vert^2 - 1) $$. Les valeurs propres de $$ M_g $$ sont $$ e^{i \theta} $$ et $$ e^{-i \theta} $$. On note $$ \vert v_+ \rangle $$ et $$ \vert v_- \rangle $$ les vecteurs propres associés.

Comme F est un espace vectoriel de dimension 2, on peut identifier $$ \vert m \rangle $$ à $$ \vert 0 \rangle $$ et $$ \vert s \rangle $$ à $$ \bar{\alpha} \vert 0 \rangle + \sqrt{1 - \vert \alpha \vert^2} \vert 1 \rangle) $$. Cette transformation préserve la valeur du produit Hermitien $$ \langle s \vert m \rangle $$ et permet de se ramener aux notations utilisées pour un qubit. Pour revenir à l'espace F (avec pour base $$ (\vert m \rangle, \vert s \rangle) $$ dans cet ordre), nous aurons besoin de la transformation inverse :

$$ \begin{align*}
\begin{pmatrix}
1 & \bar{\alpha} \\
0 & \sqrt{1 - \vert \alpha \vert^2}
\end{pmatrix}^{-1} 
&= \frac{1}{\sqrt{1 - \vert \alpha \vert^2}} \begin{pmatrix}
\sqrt{1 - \vert \alpha \vert^2} & - \bar{\alpha} \\
0 & 1
\end{pmatrix} \\
&= \begin{pmatrix}
1 & \frac{- \bar{\alpha}}{\sqrt{1 - \vert \alpha \vert^2}} \\
0 & \frac{1}{\sqrt{1 - \vert \alpha \vert^2}}
\end{pmatrix}
\end{align*} $$

On introduit donc le vecteur correspondant à $$ \vert 1 \rangle $$. On aurait également pu trouver ce vecteur en retirant à $$ \vert s \vert $$ la quantité de $$ \vert m \rangle $$ suffisante pour obtenir un vecteur orthogonal à $$ \vert m \rangle $$ :

$$ \vert x \rangle = \frac{ - \bar{\alpha}}{\sqrt{1 - \vert \alpha \vert^2}} \vert m \rangle + \frac{1}{\sqrt{1 - \vert \alpha \vert^2}} \vert s \rangle. $$

Dans la base orthonormée $$ (\vert m \rangle, \vert x \rangle) $$, la matrice de $$ U_g $$ est :

$$ \begin{align*}
M_{g, (\vert m \rangle, \vert x \rangle)} &= \begin{pmatrix}
1 & \bar{\alpha} \\
0 & \sqrt{1 - \vert \alpha \vert^2}
\end{pmatrix} 
\begin{pmatrix}
-1 & - 2 \bar{\alpha}  \\
2 \alpha & 4 \vert \alpha \vert^2 - 1
\end{pmatrix}
\begin{pmatrix}
1 & \frac{- \bar{\alpha}}{\sqrt{1 - \vert \alpha \vert^2}} \\
0 & \frac{1}{\sqrt{1 - \vert \alpha \vert^2}}
\end{pmatrix} \\

&= \begin{pmatrix}
1 & \bar{\alpha} \\
0 & \sqrt{1 - \vert \alpha \vert^2}
\end{pmatrix} 
\begin{pmatrix}
-1 & \frac{- \bar{\alpha}}{\sqrt{1 - \vert \alpha \vert^2}}  \\
2 \alpha & \frac{2 \vert \alpha \vert^2 - 1}{\sqrt{1 - \vert \alpha \vert^2}}
\end{pmatrix} \\

&= \begin{pmatrix}
2 \vert \alpha \vert^2 - 1 & -2 \bar{\alpha} \sqrt{1 - \vert \alpha \vert^2} \\
2 \alpha \sqrt{1 - \vert \alpha \vert^2} & 2 \vert \alpha \vert^2 - 1
\end{pmatrix} \\

&= \begin{pmatrix}
\cos \theta & - e^{-i \phi} \sin \theta \\
e^{i \phi} \sin \theta & \cos \theta
\end{pmatrix} \\
\end{align*} $$

L'angle $$ \phi $$ est défini par $$ \alpha = e^{i \phi} \vert \alpha \vert $$. On peut s'en débarasser en multipliant $$ \vert x \rangle $$ par cette phase :

$$ \begin{align*}
\vert y \rangle &:= e^{i \phi} \vert x \rangle \\
&= \frac{ - \vert \alpha \vert}{\sqrt{1 - \vert \alpha \vert^2}} \vert m \rangle + \frac{e^{i \phi}}{\sqrt{1 - \vert \alpha \vert^2}} \vert s \rangle.
\end{align*} $$

Dans la base $$ (\vert m \rangle, \vert y \rangle) $$, $$ U_g $$ est représentée par une matrice de rotation:

$$ \begin{align*}
M_{g, (\vert m \rangle, \vert y \rangle)} &=  \begin{pmatrix}
\cos \theta & - \sin \theta \\
\sin \theta & \cos \theta
\end{pmatrix} \\
\end{align*} $$

On peut donc se représenter l'oracle de Grover comme une rotation d'angle $$ \theta $$ avec :

$$ \begin{align*}
\cos \theta &= - 1 + 2 \vert \alpha \vert^2 \\
&= - 1 + \frac{2}{2^{n}}.
\end{align*} $$

$$ \begin{align*}
\sin \theta &= 2 \vert \alpha \vert \sqrt{1 - \vert \alpha \vert^2} \\
&= \frac{2}{\sqrt{2^{n}}} \sqrt{1 - \frac{1}{2^n}} .
\end{align*} $$

Multiplier $$ U_g $$ par une phase globale de -1 revient à changer $$ \theta $$ en $$ \theta + \pi $$. De plus changer l'ordre des vecteurs de la base revient à changer $$ \theta $$ en $$ - \theta $$. On peut donc choisir de remplacer $$ \theta $$ par $$ \tilde{\theta} := \pi - \theta $$. 

$$ \begin{align*}
\cos \tilde{\theta} &= 1 - 2 \vert \alpha \vert^2 \\
&= 1 - \frac{2}{2^{n}}.
\end{align*} $$

$$ \begin{align*}
\sin \tilde{\theta} &= 2 \vert \alpha \vert \sqrt{1 - \vert \alpha \vert^2} \\
&= \frac{2}{\sqrt{2^{n}}} \sqrt{1 - \frac{1}{2^n}} .
\end{align*} $$

En général, on utilise plutôt l'angle moitié $$ \tilde{\theta}/2 $$ :

$$ \begin{align*}
\cos \tilde{\theta}/2 &= \sqrt{1 - \vert \alpha \vert^2} \\
&= \sqrt{1 - \frac{1}{2^{n}}}.
\end{align*} $$

$$ \begin{align*}
\sin \tilde{\theta}/2 &= \vert \alpha \vert \\
&= \frac{1}{\sqrt{2^{n}}}.
\end{align*} $$

<!-- Les vecteurs propres de $$ U_g $$ peuvent être obtenus à partir de $$ \vert m \rangle $$ et de $$ \vert y \rangle $$:

$$ \begin{align*}
\vert v_+ \rangle :&= \frac{1}{\sqrt{2}} (\vert m \rangle + \vert y \rangle) \\
&= \frac{1}{\sqrt{2(1 - \vert \alpha \vert^2)}} ( - \vert \alpha \vert \, \vert m \rangle + e^{i \phi} \vert s \rangle)
\end{align*} $$

Vérifions que c'est bien un vecteur propre :

$$ \begin{align*}
U_g \vert v_+ \rangle &= \frac{1}{\sqrt{2(1 - \vert \alpha \vert^2)}} ( - \vert \alpha \vert \, ( - \vert m \rangle + 2 \alpha \vert s \rangle) + e^{i \phi} ((4 \vert \alpha \vert^2 - 1) \vert s \rangle - 2 \bar{\alpha} \vert m \rangle)) \\
& = \frac{1}{\sqrt{2(1 - \vert \alpha \vert^2)}} ( - \vert \alpha \vert \, \vert m \rangle + (2 \vert \alpha \vert \alpha - e^{i \phi}) \vert s \rangle)
\end{align*} $$ -->

## Grover avec plusieurs états marqués

On suppose maintenant que plusieurs états de la base computationnelle sont marqués :

$$ R_m = I - \sum_{j=1}^{k} \vert m_j \rangle \langle m_j \vert $$.

On peut considérer le vecteur $$ \vert o \rangle $$ qui appartient à $$ \text{Vect} ( \vert m_1 \rangle, ..., \vert m_k \rangle, \vert s \rangle) $$ et est orthogonal à tous les $$ \vert m_j \rangle $$ :

$$ \vert o \rangle = \frac{1}{\sqrt{2^n - k}} \sum_{i \neq m_1, ... m_k} \vert i \rangle. $$

$$ U_g := R_m R_s $$ est une rotation d'angle $$ \theta $$ égal au double de l'angle entre $$ \vert o \rangle $$ et $$ \vert s \rangle $$ :

$$ \begin{align*}
\cos (\theta/2) &= \frac{2^n -k}{\sqrt{2^n} \sqrt{2^n - k}} \\
                &= \sqrt{\frac{2^n -k}{2^n}}
\end{align*}. $$

$$ \sin (\theta/2) = \sqrt{\frac{k}{2^n}}. $$

De plus $$ \vert o \rangle $$ et $$ \vert s \rangle $$ sont sur la même orbite de rotation de $$ U_{\theta} $$. On peut initialiser l'algorithme en préparant le vecteur $$ \vert s \rangle $$. Le vecteur cible $$ \vert t \rangle $$ qui appartient à $$ \text{Vect} ( \vert m_1 \rangle, ..., \vert m_k \rangle) $$ et est également sur l'orbite de rotation de $$ \vert s \rangle $$ pour $$ U_g $$ est la superposition uniforme de tous les $$ \vert m_j \rangle $$ :

$$ \vert t \rangle = \frac{1}{\sqrt{k}} \sum_{j=1}^k \vert m_j \rangle. $$