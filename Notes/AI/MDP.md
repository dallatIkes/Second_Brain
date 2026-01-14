---
aliases:
  - Markov Decision Process
  - processus de décision markovien
---
---

# Markov Decision Process

Un [[MDP|processus de décision markovien]] est défini par :
- un **ensemble d'états** : $S$
- un **ensemble d'actions possibles** à l'état $s$ : $A(s)$
- un **modèle probabiliste de transition** : $P(s'\vert s,a)$ (où $a\in A(s)$)
- une **fonction de récompense** : $R(s)$ 

## Politique

Une **policy** (ou plan) est un choix d'action pour chaque état (*if state then action*).

## Fonction de récompense

Une **fonction de récompense** assigne un réel à chaque état en fonction de son degré de désirabilité.
La qualité d'un plan est déterminée par l'espérance de ses récompenses. Un plan optimal maximise ces dernières.
Un plan fait un **compromis** entre : la maximisation de la **probabilité d'atteindre le but** et la maximisation des **récompenses**.

## Utilité

L'**utilité** d'un plan $\pi$ exécuté à partir d'un état $s$ est donnée par : $$
\begin{align}
U^\pi(s) &= \mathbb{E}[\sum_{t=0}^\infty\gamma^tR(s_t,\pi(s)),s_{t+1}] \\ 
&=  \sum_{s'\in S}P(s'\vert s,\pi(s))[R(s,\pi(s),s')+\gamma U^\pi(s')]
\end{align}$$avec :
- $\gamma$ : facteur d'escompte ($0\le\gamma\le1$) (but : pondérer les récompenses en fonction de la distance à l'horizon : plus $\gamma$ est petit, plus l'horizon est proche) $\rightarrow$ assure la convergence
- $R(s,a,s')$ : récompense pour la transition $(s,a,s')$
- $S$ : espace d'états
- $\pi(s)$ : action du plan à l'état $s$
- $P(s'\vert s,\pi(s))$ : probabilité pour la transition du [[MDP]] 

On dit qu'un plan $\pi$ en domine un autre $\pi'$ si $\forall s,U^\pi(s)\ge U^{\pi'}(s)$ et pour au moins un $s$ $E^\pi(s)\gt U^{\pi'}(s)$. Une policy est optimale si elle n'est dominée par aucune autre ([[Relation d'ordre|relation d'ordre]] partiel)

Il existe deux algorithmes pour le calcul de la policy optimale : 
- **value iteration**
- **policy iteration** 

### Équations de Bellman

**Utilité d'un état :** $U^*(s)=\underset{a\in A(s)}{\max}\sum_{s'\in S}P(s'\vert s,a)[R(s,a,s')+\gamma U(s')]$  
**Plan optimal :** $\underset{a\in A(s)}{\arg\max}\sum_{s'\in S}P(s'\vert s,a)[R(s,a,s')+\gamma U(s')]$ 

### Fonction action-utilité (Q-function)

$Q(s,a)=\sum_{s'\in S}P(s'\vert s,a)[R(s,a,s')+\gamma U(s')]$ 
ainsi $Q(s,a)=\sum_{s'\in S}P(s'\vert s,a)[R(s,a,s')+\gamma\underset{a'\in A(s')}{\max}Q(s',a')]$ 
On a donc : 
- $U^*(s)=\underset{a\in A(s)}{\max}Q(s,a)$ 
- $\pi^*(s)=\underset{a\in A(s)}{\arg\max}Q(s,a)$ 
### Algorithme Value Iteration

1. Initialiser $U(s)$ à $0$ pour chaque état $s$
2. Répéter jusqu'à ce que le changement soit négligeable :
		$U\leftarrow\underset{a}{\max}Q(s,a)$ 
3. Définir le plan optimal en choisissant pour chaque état $s$ la meilleure action $a$
		$\pi(s)=\underset{a}{\arg\max}Q(s,a)$ 
On choisit l'action qui maximise l'espérance des sommes des récompenses futures
**Complexité :** $O(\lvert S\rvert^4\lvert A\rvert^2)$ 

### Algorithme Policy Iteration

1. Choisir un plan arbitraire $\pi'$
2. Répéter jusqu'à convergence de $\pi$ :
	1. $\pi \leftarrow \pi'$ 
	2. $\forall s\in S$, résoudre le système de $\lvert S\rvert$ équations et $\lvert S\rvert$ inconnues pour calculer $U^\pi(s)$ 
	3. $a^*=\underset{a\in A(s)}{\arg\max}Q(s,a)$ et si $Q(s,a^*)\gt Q(s,\pi(s))$ alors $\pi'(s)\leftarrow a^*$ sinon $\pi'(s)\leftarrow \pi(s)$ 
3. Retourner $\pi$
