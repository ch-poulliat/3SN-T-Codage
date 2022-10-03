## Codes en blocs linéaires

### Définition

On considèrera des codes de canal définis sur $\mathbb{F}_2=GF(2)$.

```{prf:definition} Codes linéaires en bloc

Un code en bloc binaire $\mathcal{C}(N,K)$ de *longueur* $N$ et de*dimension* $K$ est une application $g(.)$ de l'ensemble
$\mathbb{F}_2^K =\{0, 1 \}^K$ vers l'ensemble $\mathbb{F}_2^N =\{0, 1\}^N$ qui associe à tout bloc de données
d'information $\bf{u}$ un mot de code $\bf{c}$. 

$$\begin{aligned}
g : \mathbb{F}_2^K & \rightarrow & \mathbb{F}_2^N \nonumber \\
{\bf u} & \mapsto & {\bf c} = g({\bf u})
\end{aligned}$$

$\mathcal{C}(N,K)$ est dît linéaire si $g(.)$ est une application linéaire.
```

Pour un code linéaire, le nombre de mots de code est $2^K$ et forme un sous-espace vectoriel de $\mathbb{F}_2^N$. De plus, toute combinaison
linéaire de mots de code est un mot de code de $\mathcal{C}(N,K)$. On définit le rendement de codage comme le rapport entre le nombre $K$ de
symboles d'information divisé par le nombre $N$ de symboles codés :

$$R = \frac{K}{N}$$

On adoptera les notations vectorielles suivantes ${\bf c}=[c_0, \ldots, c_{N-1}]$ et ${\bf u}=[u_0, \ldots, u_{K-1}]$.

### Matrice génératrice

```{prf:definition} Matrice génératrice

La matrice génératrice $\mathbf{G}$ de dimensions $K \times N$ est lamatrice associée à l'application linaire $g$ définie comme

$${\bf c}= {\bf u} \mathbf{G}.$$ 

L'espace image du code est alors défini par

$\mathrm{Im}(\mathcal{C})=\{ {\bf c} \in \mathbb{F}_2^N | {\bf c}= {\bf u} \mathbf{G}, \;\; \forall {\bf u} \in \mathbb{F}_2^K \}$
```

On a alors les propriétés suivantes :

```{prf:property}
1.  $\mathrm{rang}(G)=K$,

2.  les lignes de $\mathbf{G}$ sont $K$ mots de codes indépendants,

3.  $\mathbf{G}$ n'est pas définie de manière unique (pourquoi?),

4.  $\mathbf{G}$ est dite systématique si     $\forall k \in [0,K-1], \exists n \in [0,N-1]$ tel que $c[n]=u[k]$.
    $\mathbf{G}$ peut alors se mettre sous la forme
    
    $$\mathbf{G}=[P |I_K ]$$

5.  Pour chaque coordonnée d'un mot de code de $\mathcal{C}(N,K)$, la     probabilité d'occurrence d'un $'1'$ ou d'un $'0'$ est identique si
    la génération de l'information est i.i.d.

### Matrice de parité

```{prf:definition} Code dual et matrice de parité

Le code $\mathcal{C}^{\bot}(N-K,K)$, dît code dual, vérifie que tout mot du code dual est orthogonal à tout mot du code $\mathcal{C}(N,K)$. On
note une matrice génératrice pour ce code ${\bf H}$. On a alors

$$\{ {\bf c} \in \mathcal{C}(N,K) | {\bf c} \mathbf{H}^{\top} = {\bf 0} \}$$
```

Ainsi, on a tous les bits d'un mot de code ${\bf c}$ vérifie un jeu de contraintes linéaires appelées ***équations de parité***. 


```{prf:property}
-   Relation avec ${\bf G}$ : 

$${\bf G}{\bf H}^{\top}={\bf 0}$$

-   Pour un code systématique défini par $\mathbf{G}=[P |I_K ]$, on a

    $$\mathbf{H} =[I_{N-K} | P^{\top}].$$
```
On peut également utiliser la matrice de parité pour la détection d'erreur à l'aide du ***syndrome***. Soit ${\bf r}={\bf c}+{\bf e}$ où
${\bf r}$ est le mot reçu et ${\bf e}$ le vecteur de bruit. Alors

$${\bf s}={\bf r}{\bf H}^{\top}={\bf e}{\bf{H}}^{\top}$$

Si ${\bf e}$ n'est pas un mot de code alors, une erreur est détecter car le syndrome est non nul dans ce cas. Si ${\bf e}$ est un mot de code,
alors on parle d'erreurs *non détectable* (syndrome nul).

### Distance minimum et spectre de distance


```{prf:definition} Poids de Hamming
On appelle poids de Hamming d'un mot de code ${\bf c} \in \mathbb{F}_2^n$ le nombre de coordonnées non nulles de ce
vecteur. On notera

$$w({\bf c})= \sum_{k=0}^{n-1} \delta{(c_k)},\; \text{ où } \delta(c_k)=\begin{cases}
1 &\text{ si } c_k=1 \\
0 &\text{ sinon}
\end{cases}$$
```


```{prf:definition} Distance de Hamming

La distance de Hamming entre deux mots de code est définie par

$$d_H(c_i ,c_j)=w{(c_i \oplus c_j)}$$
```

```{prf:definition} Distance minimale

La distance minimale du code $\mathcal{C}$ est donnée par

$$\begin{aligned}
d_{\min}&= &\min{\{ d_H(c_i , c_j )| c_i , c_j \in \mathcal{C}(N,K) ; c_i \neq c_j \}} \nonumber \\
& = & \min{\{\boldsymbol{\mathit{w}}(c) | c \in \mathcal{C}(N,K), c \neq 0 \}}
\end{aligned}$$
```
```{prf:definition} Spectre de poids/distances

On définit alors le *spectre de poids* d'un code par les coefficients

$$\forall i=1 \ldots N, w_i = \# {\bf c} \in  \mathcal{C}(N,K), \; \boldsymbol{\mathit{w}}(c)=i$$

Le set $\{w_0,\cdots, w_N\}$ est alors appelé la distribution des poids du code que l'on représente par le polynôme énumérateur de poids

$$W(x)=\sum_{i=0}^N{w_i x^{i}}$$
```
On peut alors remarquer que $d_{\min}$ est égale au plus petit nombre de colonnes dont la somme est le vecteur nul.

### Exemples

```{prf:example} Code de répétition
Un code de répétition consiste en la répétition de $N$ fois un bit d'information. On obtient un code $\mathcal{C}(N,1)$ de matrice
génératrice 

$$G_1=[\underbrace{1 \ldots 1 \ldots 1}_{N}]$$

```
```{prf:example} Code de vérification de parité

Un code de vérification de parité est construit tel que $c_{N-1}=u_0 \oplus u_1 \oplus \cdots \oplus u_{N-2}$ définissant un
code $\mathcal{C}(N,N-1)$. Sa matrice génératrice est alors donnée par

$$G_2=\left(\begin{array}{cccc }
 &  &  &1 \\
 &  &  & \vdots\\
 & I_{N-1} &  &1 \\
 &  &  & \vdots\\
 &  &  & 1\\
\end{array} \right)$$ 
```


On peut alors remarquer que les deux codes précédents sont duaux, ie. $$G_1G_2^{\top}={\bf 0}$$
