## Codes LDPC binaires

### Définitions et notations usuelles
De manière générale, un code LDPC dans $\mathbb{F}_Q$ (avec $Q=2^p$ ) est représenté par sa matrice de parité creuse $H$ de taille $(N-K) \times N$ dont les éléments non nuls sont des éléments du corps de Galois $\mathbb{F}_Q$ . $N$ est défini comme la longueur du mot de code, $K$ le nombre de bits d'information associés à un mot de code, $M=N-K$ le nombre de bits de redondance et $R \leq K / N$ définit le rendement du code, l'égalité étant obtenue pour une matrice $H$ de rang plein. Le code est alors défini comme l'ensemble des mots de code $\underline{x} \in \mathbb{F}_Q^K$ vérifiant $H \cdot \underline{x}=\underline{0}$. Dans le cas $Q=2$, nous retrouvons l'expression des codes LDPC binaires et leur description par des équations de contrainte de parité. Pour les cas $Q>2$, les codes appartiennent à la famille des codes LDPC non binaires. 

Dans ce chapitre, nous ne considérerons que les codes LDPC binaires. On peut alors en donner la définition formelle suivante

```{prf:definition} Codes LDPC binaires

$$\mathcal{C}_{H}=\{{\bf c} \in GF(2)^{\times N} | H.\bf{c}^\top = \bf{0}\}$$

-   $H$ est la matrice de parité du code de taille $M \times N$,

-   Si $H$ de rang plein : $R=K/N$ avec $K=N-M$,

-   Equations de parité :
    $\bigoplus_{j: h_{ij}\neq 0} c_j=0, \;\; \forall i=1 \ldots M$,

-   $H$ est dîte à faible densité si

    $$\frac{\mbox{ éléments non nuls }}{N.M} \underset{N \mapsto + \infty}{\longrightarrow} 0$$
:::
```


### Graphe de Tanner

De manière équivalente, un code LDPC peut être représenté par un graphe bi-nodal, communément appelé graphe factoriel graphe de Tanner. Ce graphe est composé de deux types de nœuds: 

- ***des nœuds de variables*** représentant les bits du mot de code
- ***des nœuds de contraintes de parité*** représentant les fonctions de vérification de parités. 

Les nœuds de variables et de contraintes de parité sont connectés entre eux par ***des branches*** qui indiquent à quelles équations de parité participent les différents nœuds de variables et donc les bits associés. Ainsi le $n$-ième nœud de variable et le $m$-ième nœud de contrainte de parité seront connectés si $H_{n, m}=1$. On appellera degré de connection d'un nœud de variable (idem pour un nœud de contrainte de parité) le nombre de branches connectées à ce nœud. Un nœud sera dit de degré $i$ s'il est connecté à $i$ branches. 

```{prf:example} 
La figure 4-2 nous donne la représentation d'un code régulier de paramètres $\left(N=8, d_v=2, d_c=4\right)$. Les deux premières représentations sont les représentations équivalentes d'un code particulier à l'aide de sa matrice de parité et du graphe factoriel associé. Ce code est issu de la famille de codes paramétrée par $\left(N=8, d_v=2, d_c=4\right)$ et dont la représentation est donnée par le troisième graphe de la figure 4-2. Un code correspond alors à une réalisation particulière de l'entrelaceur.
```


### Codes LDPC Réguliers 
Un code LDPC régulier paramétré par le triplet $\left(N, d_v, d_c\right)$ est défini par une matrice comportant exactement $d_v$ (respectivement $d_c$) '1' par colonne (respectivement par ligne). Le rendement est alors donné $R \leq K / N=1-d_v / d_c$, l'égalité étant obtenue pour une matrice $H$ de rang plein. Notons que, si l'on considère la famille des codes LDPC réguliers de paramètres $\left(N, d_v, d_c\right)$, un code issu de cette famille est donné par une représentation particulière de la matrice de parité. Un code sera dit régulier si le nombre d'éléments par ligne (respectivement par colonne) est constant. 


### Codes LDPC irréguliers 

Un code est dit irrégulier, s'il n'est pas régulier. La représentation usuelle des codes LDPC irréguliers est réalisée à l'aide des deux polynômes suivants:

- Polynôme associé aux nœeuds de variables:

$$
\lambda(x)=\sum_{i=2}^{d_v} \lambda_i x^{i-1}
$$

où $\lambda_i$ est la proportion de branches du graphe connectées à un nœud de variable de degré i. $d_v$ est le nombre maximum de branches connectées à un nœud de variable.

- Polynôme associé aux nœuds de contrainte de parité :

$$
\rho(x)=\sum_{j=2}^{d_c} \rho_j x^{j-1}
$$

où $\rho_j$ est la proportion de branches du graphe qui sont connectées à un nœud de contrainte de parité de degré $j . d_c$ est le nombre maximum de branches connectées à un nœud de contrainte de parité.

Ces deux quantités sont reliées par le rendement du code donné par

$$
R=1-\frac{\sum_{j=2}^{d_c} \rho_j / j}{\sum_{i=2}^{d_v} \lambda_i / i}
$$

Il existe également une représentation duale qui nous sera utile par la suite donnée par:

- Polynôme associé aux nœuds de variables :

$$
\tilde{\lambda}(x)=\sum_{i=2}^{d_v} \overline{\lambda_i} x^{i-1}
$$

où $\bar{\lambda}_i$ est la proportion de nœuds de variables du graphe de degré $i$.

- Polynôme associé aux nœuds de contrainte de parité :

$$
\tilde{\rho}(x)=\sum_{j=2}^{d_c} \tilde{\rho}_j x^{j-1}
$$

où $\tilde{\rho}_j$ est la proportion de nœuds de contraintes de parité du graphe de degré $j$.
Le passage de l'une à l'autre des représentations est alors assuré par les équations suivantes

$$
\begin{array}{ll}
\bar{\lambda}_i=\frac{\lambda_i / i}{\sum_k \lambda_k / k} & \tilde{\rho}_j=\frac{\rho_i / j}{\sum_k \rho_k / k} \\
\lambda_i=\frac{i \bar{\lambda}_1}{\sum_k k \lambda_k} & \rho_j=\frac{j \bar{\rho}_j}{\sum_k k \bar{\rho}_k}
\end{array}
$$

Ainsi une famille de codes irréguliers est paramétrée par le triplet $(N, \lambda(x), \rho(x))$. Le cas régulier est un cas particulier de cette représentation où $\lambda(x)$ et $\rho(x)$ sont mono-degré. Le jeux de paramètres $(\lambda(x), \rho(x))$ définit ce que l'on appelle le profil d'irrégularité du code suivant les colonnes et suivant les lignes respectivement.

### Exemple du code de Hamming

On illustre ici le cas d'une matrice de parité d'un code de Hamming, qui n'est cependant pas une exemple parfait de codes LDPC, mais cela permet d'illustrer facilement les précédentes notions.


