# Introduction à la théorie de l'information

La théorie de l'information introduite par Claude Shannon en 1948 permet de définir un cadre théorique qui permet d'analyser les performances limites d'un système de communication. En utilisant un cadre probabiliste pour l'analyse des performances d'un système de
communication, Shannon a montré que l'on pouvait séparer ***asymptotiquement*** le problème de transmission d'une source au travers
d'un canal de communication physique point-à point en deux grande classes de problèmes : (a) la mise en forme de la source puis (b) la
transmission sur le canal. Ces deux grandes étapes sont associées à deux grands domaines de l'ingéniérie des communications numériques :
compression de source (voir cours 2A et 3A) et le codage de canal. Une représentation de la vision initiale d'une chaîne de communication dîte point-à-point est alors donnée figure [5.0.1](#){reference-type="ref" reference=""}. On remarquera qu'à l'époque la couche réseau n'était pas considéré, ces derniers n'apparaissant que fin des années 60. Alors que la compression (encore appelée codage de source avec ou sans perte) s'intéresse à la représentation d'une source (analogique discrétisée le plus souvent) par une séquence de bits permettant de s'approcher de l'entropie minimale associée à cette source pour une distorsion donnée, la théorie du codage canal permet elle d'introduire une redondance structurée de l'information compressée afin de corriger des erreurs et de permettre d'opérer le plus proche possible de ce que l'on appellera la capacité du canal.

## Notion de source 

Par ma suite, on traitera essentiellement des sources d'information qui seront modélisée par un processus aléatoire. Une ***source d'information*** est donc représentée par une suite de symboles $(X_0, X_1, \cdots, X_n, \cdots)$. Chaque symbole $X_i$ appartient à un
alphabet discret $\mathcal{X}$, de cardinalité finie. $X_i$ est associée à une variable aléatoire et donc $\{X_n\}_{n \in \mathbb{N}}$ définit un processus aléatoire. On suppose défini

$$
p(X_0=x_0, \cdots X_1=x_1, \cdots , X_n=x_n), \; \forall n.
$$ 


Une source d'information est dîte *stationnaire* si toute distribution deprobabilité de symboles est invariante par translation temporelle, ie.

$$\forall n, \forall l, \forall (x_0,x_1,\cdots, x_n)\in \mathcal{X}^n,  p(X_0=x_0, \cdots, X_n=x_n)=p(X_{0+l}=x_0, \cdots, X_{n+l}=x_n).$$ 

Une source stationnaire est dîte sans mémoire si les symboles $X_n$ sont produits de manière indépendante des symboles source passés, ie. $X_i, \; \forall i=0 \cdots n-1$. On a ainsi

$$p(X_n|X_{n-1} \cdots X_0)=p(X_n).$$ 

On en déduit

$$p(X_0,\cdots,X_n)=p(X_0)\cdots p(X_n).$$ 

On a donc les symboles $X_i$
indépendants et par stationnarité, les $X_i$ sont identiquement
distribués.

```{prf:definition} Source sans mémoire
Une source sans mémoire est définie par une suite de symboles $X_0,\; X_1, \cdots X_n$ indépendants et identiquement distribués (on
parle de processus aléatoire à variables aléatoires i.i.d.).
```

Pour une source discrète sans mémoire, $X$ une variable aléatoire discrète à valeurs dans l'alphabet $\mathcal{X}$ de d.d.p. discrète
$p(x)=\operatorname{Prob}(X=x), x \in \mathcal{X} .$ Une source discrète sans mémoire produit une séquence de symboles i.i.d. à valeurs dans $\mathcal{X}$ et suivant $p(x).$ Un exemple est une source de symboles issus d'une constelationn $M$-aire.

Pour une source continue sans mémoire, $X$ une variable aléatoire pouvant prendre des valeurs réelles dans un intervalle
$\mathcal{X} \subset \mathbb{R}$ de d.d.p. $f(x) .$ Une source (absolument) continue sans mémoire produit une séquence de symboles
i.i.d à valeurs dans $\mathcal{X}$ et suivant la d.d.p. $f(x)$. Un exemple classique est donné par un processus Gaussien.

## Notion de canal 

Le canal de transmission sera caractérisé par une approche probabiliste pour la modélisation. Pour un ***canal discret sans mémoire***, on émet un symbol $X=x$ où $X \in \mathcal{X}$ est une valeur aléatoire à valeur dans un alphabet fini et caractérisé par une distribution des symboles $p(x).$ A la sortie du canal on observe la $Y=y$ qui peut être à valeur soit dans un alphabet discret ou appartenir à un sous ensemble $\mathcal{I} \in \mathbb{R} \text{ ou } \mathbb{C}$. La définition du canal se fait au travers de ce que l'on appelle la probabilité de transition du canal donnée par la vraisemblance $p(y \mid x)$. Elle représente la probabilité de recevoir $Y=y$ sachant que l'on a émis $X=x$. Si $X$ est une variable aléatoire (v.a.) $M$ -aire et Y une v.a. $N$-aire, on appelle matrice de transition du canal la matrice de taille $N \times M$ donnée par 

$$
\Pi=(p(y \mid x))_{y, x}.
$$ 

La somme de chaque colonne de $\Pi$ vaut 1 et on a 

$$p_{Y}=\Pi p_{X}$$ 

avec $p_{Y}=(p(y))_{y}$ et $p_{X}=(p(x))_{x}$ vecteurs colonnes.

