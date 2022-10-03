## Décodage par propagation de croyance

Si il est possible de décoder les codes LDPC au sens du maximum de vraisemblance, la complexité devient trop importante dès lors que l'on considère des mots de code de tailles significatives, hypothèse importante pour obtenir des performances convenables. L'algorithme pratique sous optimal mise en oeuvre est connu sous le nom d'algorithme de ropagation de croyances (Belief Propagation, BP) ou algorithme Somme-Produit (Sum-Product). Comme son nom l'indique, cet algorithme propage le long des branches du graphe associé au code des ***messages par nature extrinsèques***. A chaque branche sont associés deux messages, un dans chaque direction de propagation de l'information. Le principe de la propagation de croyance est l'application de la règle de Bayes localement (sur chaque nœud fonctionnel du graphe) et on réalise un décodage distribué de manière itérative afin d'estimer les probabilités a posteriori de chaque bit. Il a été montré que sur un graphe sans cycle (le graphe est alors un arbre), que la factorisation locale des règles de Bayes conduit au calcul exact des probabilités a posteriori des nœuds de variables. Dans ce cas, les messages transitant sur le graphe sont tous indépendants. Cependant, dans le cas de graphes avec cycles (ce qui est le cas des codes LDPC à taille finie), la dépendance des messages résultante ne permet plus d'assurer le calcul exact des probabilités a posteriori, ce qui induit une sous-optimalité de l'algorithme dans ce contexte.

Les messages transitant sur les branches du graphe sont généralement des vecteurs de probabilités. Cependant, dans le cas binaire, on peut utiliser comme représentation des messages une représentation mono-dimensionnelle donnée grâce à l'utilisation des log-rapports de vraisemblances (log likelihood ratio, LLR). Nous présentons maintenant l'algorithme BP en prenant une représentation à l'aide des LLR. Nous noterons $v=\log \left(\frac{p(c=0 \mid\{z\})}{p(c=1 \mid\{z\})}\right)$, le message de sortie sur une branche d'un nœud de variable et $u=\log \left(\frac{p\left(c^{\prime}=0 \mid\left\{z^{\prime}\right\}\right)}{p\left(c^{\prime}=1 \mid\left\{z^{\prime}\right\}\right)}\right)$ le message de sortie sur une branche d'un nœud de contrainte de parité. $\{z\}$ (resp. $\left.\left\{z^{\prime}\right\}\right)$ représente l'ensemble des messages entrant sur un nœud de variable (resp. nœud de contrainte de parité) hormis la branche de de sortie considérée.

### Algorithme BP
Pour l'algorithme BP, chaque itération $\ell$ de décodage est composée de deux étapes:

- ***Mise à jour des noeuds de variables (pour un nœud de degré $i$ ) :***

$$
v_m^{(l)}=u_0+\sum_{k=1, k \neq m}^i u_k^{(l-1)}, \forall m=1 \ldots i
$$

$v_m$ est le message (LLR) de la m-ième branche à la sortie d'un nœud de variable. Les messages $u_k$ sont les LLR à l'entrée d'un nœud de variable et $u_0$ est le LLR de l'observation du canal. A la première itération, tous les messages $u_k^{(0)}$ sont nuls. On a également $u_0=$ $\log \left(\frac{p(x=0 \mid y)}{p(x=1 \mid y)}\right)=\log \left(\frac{p(y \mid x=0)}{p(y \mid x=1)}\right)$ si $x$, qui représente un bit du mot de code, est une variable aléatoire équi-distribuée à valeur dans $\{0,1\}$.


- ***Mise à jour des nœuds de contraintes de parité (pour un nœud de degré $j$) :***

$$
\tanh \frac{u_k^{(l)}}{2}=\prod_{m=1, m \neq k}^j \tanh \frac{v_m^{(l)}}{2}, \forall k=1 \ldots j
$$

$u_k$ est le message (LLR) de la k-ième branche à la sortie d'un nœud de contrainte de parité.
Les messages $v_m$ sont les LLR à l'entrée d'un nœud de contrainte de parité. Une itération de l'algorithme de propagation de croyance est réalisée lorsque tous les messages dans le graphe ont été calculés une fois à l'aide des équations précédentes. Après $L$ itérations, pour la décision, il est possible de calculer le rapport a posterioti pour chacun des nœuds de variable qui sera donné par

$$
v_{\text {app }, n}=u_0+\sum_{k=1}^i u_k^{(L)}, \forall n=1 \ldots N
$$


- ***Décision finale :***

Et finalement la décision sur la valeur binaire est donnée pour chaque nœud de variable par

$$
\hat{m}_n=\frac{1-\operatorname{sign}\left(v_{\mathrm{app}, n}\right)}{2}, \forall n=1 \ldots N
$$

### Algorithmes à faible complexité

```{prf:defintion} Algorithme BP simplifié : Min-Sum 

$$u_k^{(l)}=\left[\prod_{m=1,m \neq k}^{j}{\mathrm{sign}{(v_m^{(l)})}}\right] \left[\min_{m \neq k}{( |v_m^{(l)}|)}\right] \mbox{, }\forall k=1 \ldots j$$
```

```{prf:defintion} Algorithme Min-Sum atténué


$$u_k^{(l)}= \alpha_k^{(l)} \left[\prod_{m=1,m \neq k}^{j}{\mathrm{sign}{(v_m^{(l)})}}\right] \left[\min_{m \neq k}{( |v_m^{(l)}|)}\right] \mbox{, }\forall k=1 \ldots j$$
$0 < \alpha <1$ est un facteur d'atténuation, éventuellement variable.
```

```{prf:defintion} Algorithme Min-Sum avec offset


$$u_k^{(l)}= \left[\prod_{m=1,m \neq k}^{j}{\mathrm{sign}{(v_m^{(l)})}}\right] \left[\max{\left\{\min_{m \neq k}{(|v_m^{(l)}|)} - \beta,0 \right\}}\right] \mbox{, }\forall k=1 \ldots j$$

$0 < \alpha <1$ est un facteur d'atténuation, éventuellement variable.
```
