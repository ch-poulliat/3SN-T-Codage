## Décodage MAP symbole

### Critère MAP bit

On s'intéresse ici au décodage des codes convolutifs suivant un critère MAP symbole, le symbole étant ici un bit. Ce critère diffère du MAP séquence ou ML. L'idée ici est de calculer la probabilité a posteriori d'un bit d'information (ou codé comme on le verra après) sachant l'ensemble de observations. Ceci est donné par la définition suivante si
on considère une séquence de bits d'information $u_n \in \{ 0,1 \}$ de taille $K$


```{prf:definition} Critère MAP bit

$$\begin{aligned}
\hat{u}_n &=& \mathrm{arg} \max_{u_n}{p(u_n | {\bf y}) } \nonumber \\
&=& \frac{1-\mathrm{signe}(L(u_n))}{2}
\end{aligned}$$ 

avec

$$L(u_n)=\log{\left[\frac{p(u_n = 0 | {\bf y})}{p(u_n = 1 | {\bf y})}\right]}$$
```

La quantité $L(u_n)$ est ce que l'on appelle le LLR (*Log-Likelihood Ratio*) associé au bit $u_n$.

Le critère est une conséquence du fait que l'on considère une variable binaire. En effet, si on considère le bit $u_n$, alors le test de
décision statistique binaire associé donne 

$$\hat{u}_n = \mathrm{arg} \max_{u_n}{p(u_n | {\bf y}) }=0$$ 

si

$$p(u_n=0 | {\bf y}) > p(u_n=1 | {\bf y}).$$

Par passage au $\log$ et définition du LLR associé à $u_n$ on obtient alors $L(u_n)>0$. De la même manière, on aura $\hat{u}_n =1$ si
$L(u_n)<0$. On a donc la relation $\mathrm{signe}(L(u_n))=1-2 u_n$ qui nous définit un mapping bijectif entre le signe du LLR et la valeur
binaire. Ce mapping bijectif correspond d'ailleurs à un mapping de type BPSK : $\{`0' \leftrightarrow +1, `1' \leftrightarrow -1 \}$. Compte
tenu de cette relation directe, il est souvent plus commode de directement considérer la version \"mappée/modulé\" du bit (cas des
canaux souples), de sorte que l'on considérera de manière indifférenciée $u_n=0/1$ et $u_n=\pm 1$ dès lors le contexte en suffisamment clair.
Ainsi, on pourra adopter la règle MAP suivante

$$\begin{aligned}
\hat{u}_n &=\mathrm{arg} \max_{u_n}{p(u_n | {\bf y}) } \nonumber \\
&= \mathrm{signe}(L(u_n))
\end{aligned}$$

Le LLR associé à $u_n$ peut être associé à une mesure de fiabilité de la décision. En effet, $\mathrm{signe}(L(u_n))$ est identifiable à une
décision \"dure\" du bit à laquelle on peut associer une mesure de fiabilité de cette décision grâce à $|L(u_n)|$. Plus cette dernière
valeur est élevée, plus la décision est fiable. On peut également noter que la connaisance du LLR permet de remonter facilement aux probabilité
en remarquant que

$$\begin{aligned}
p(u_n =0 | {\bf y}) + p(u_n =1 | {\bf y})= 1 \\
\nonumber \\
L(u_n) = \log{\left(\frac{p(u_n = 0 | {\bf y})}{p(u_n = 1 | {\bf y})}\right)}
\end{aligned}$$

On obtient alors les relations suivantes

$$\begin{aligned}
p(u_n =0 | {\bf y}) & = & \frac{e^{L(u_n)}}{1+e^{L(u_n)}} \\
\nonumber \\
p(u_n =1 | {\bf y}) & = & \frac{1}{1+e^{L(u_n)} }
\end{aligned}$$

La quantité $L(u_n)$ est souvent appelée *information souple*. Un algorithme qui fournit en sortie des informations homogènes à des LLRs
(ou symboles bruités) est appelé *algorithme à sorties souples (Soft Outputs, SO)* par opposition à des algorithmes qui fournissent une
version décidée des symboles dénommés *algorithme à sorties dures (Hard Outputs, HO)*. Par analogie, si les entrées sont des symboles décidés,
on parle d'algorithem à entrées dures (Hard Input, HI) par opposition à des algorithmes à entrées souples (Soft Inputs, SI) prenant en compte
des symboles bruités ou des entrèes représentant des statistiques suffisantes.

### Algorithme BCJR/Forward-Backward

#### Notations

Dans la suite, nous adopterons les notations suivantes:

-   Sans perte de généralité, et pour simplifier l'exposition, on considérera un code de rendement à $1$ entrée et $nc$ sorties. Le rendement initiale avant fermeture est donc $R_0=1/n_c$.

-   La longueur totale de treillis considéré est $L=K+Nf$ ($K$ bits d'info. + $Nf$ bits de fermeture).

-   Pour simplifier l'écriture, on considérera des notations vectorielles. Ainsi le mot de code émis est ${\bf c}=[c_1, c_2, \cdots c_L]$ avec
    $c_k=[c_k^{(1)}, c_k^{(2)}, \cdots, c_k^{(n_c)}]$ le label codé émis de bits codés à l'instant $k$. De même, on a le vecteur de symboles
    bruités reçus noté par ${\bf y}=[y_1, y_2, \ldots y_L]$ avec $y_k=[y_k^{(1)}, y_k^{(2)}, \ldots, y_k^{(n_c)}]$. $y_k$ est le
    symbole reçu issu d'un canal à entrées binaires et sans mémoire. Si le canal est additif, on aura $y_k^{(j)}=c_k^{(j)}+b_k^{(j)}$, en
    supposant $c_k^{(j)}$ la version modulée du bit codé. On notera ${\bf y}_{k}^{l}=[y_k, y_{k+1}, \cdots y_{l-1}, y_{l}]$ la suite
    d'observations entre les sections $k$ et $l$.

#### LLR MAP revisité

Dans le cadre des codes convolutifs, on va maintenant dériver l'expression du critère MAP bit qui permet de calculer le critère

C'est un algorithme de type bloc qui considère un traitement par bloc des données. Pour ceci, on utilisera la représentation markovienne du
code à l'aide son espace d'état. On notera par $s_n$ l'état d'arrivée du codeur quand le bit $u_n$ a été émis. On a alors une correspondance
bijective : $u_n \leftrightarrow (s_{n-1},s_n)$. En parliculier, on aura besoin de définir les ensembles suivants:

1.  Ensemble des transitions associées à $u_n=+1$ sur une section de treillis :

    $$\mathcal{S}^{+} = \{ (s',s) \; \mathrm{ o\grave{u} } \; (s_{n-1}=s') \mapsto (s_{n}=s)| u_n=+1 \}$$

2.  Ensemble des transitions associées à $u_n=-1$ sur une section de treillis :

    $$\mathcal{S}^{-} = \{ (s',s) \; \mathrm{ o\grave{u} } \; (s_{n-1}=s') \mapsto (s_{n}=s)| u_n=-1 \}$$

On peut alors dériver l'expression du LLR $L(u_n)$ associé à la décision MAP comme suit 

$$\begin{aligned}
L(u_n)&=\log{\left[\frac{p(u_n = +1 | {\bf y})}{p(u_n = -1 | {\bf y})}\right]} \nonumber \\
&\nonumber \\
&=\log{\left[\frac{p(u_n = +1 , {\bf y})}{p(u_n = -1 , {\bf y})}\right]} \nonumber
\end{aligned}$$

On peut noter alors que pour $u_n=+1$ (résultat similaire pour $u_n=-1$), on a 

$$\begin{aligned}
p(u_n = +1, {\bf y})&= \sum_{s'}\sum_s {p(u_n = +1, s_{n-1}=s', s_{n}=s, { \bf y})}  \nonumber \\ 
&=\sum_{\mathcal{S}^{+}}{p(s_{n-1}=s', s_{n}=s, { \bf y})} \nonumber \\
\end{aligned}$$ 

et donc au final, on peut écrire 

$$\begin{aligned}
L(u_n)&=\log{\left[\frac{ \sum_{\mathcal{S}^{+}}{p(s_{n-1}=s', s_{n}=s, { \bf y})}}{\sum_{\mathcal{S}^{-}}{p(s_{n-1}=s', s_{n}=s, { \bf y})}}\right]}
\end{aligned}$$

Il nous reste alors à calculer le terme $p(s_{n-1}=s', s_{n}=s, { \bf y})$.

#### Factorisation de $p(s', s, { \bf y})$

Par application de la règle de Bayes et en utilisant les propriétés markoviennes du code, on peut écrire la factorisation suivante

$$\begin{aligned}
p(s_{n-1}=s', s_{n}=s, { \bf y})&=\alpha_{n-1}(s') \gamma_n(s',s) \beta_{n}(s) 
\end{aligned}$$ 

où 

$$\begin{aligned}
\alpha_{n}(s) &= p(s_n=s, {\bf y}_1^n) \nonumber\\
\beta_{n}(s) &= p({\bf y}_{n+1}^L|s_n=s) \nonumber\\
\gamma_n(s',s)&= p(s_n=s, y_n|s_{n-1}=s')\nonumber
\end{aligned}$$

$\alpha_{n}(s)$ représente alors la probabilité conjointe d'être dans l'état $s_n=s$ et d'avoir les observations associées aux $n$ premières
trnasitions du treillis (information du passé). cette quantité est souvent appelée *métrique forward*. De la même manière, $\beta_{n}(s)$
représente alors la probabilité d'observer les les observations futures sachant l'état $s_n=s$ (information liée aux observations futures).
cette quantité est souvent appelée *métrique backward*. Enfin, $\gamma_n(s',s)$ souvent appelé prbabilité/métrique de transition
correspond à la vraisemblance liée à l'obervation courante. Elle dépend explicitement du modèle de canal. Ainsi, de manière très grossière, le
calcul du MAP pour une section $n$ du treillis (on veut décdier le bit $u_n$) se réalise par le produit de probabilités associées à une
information du passé du future et de l'observation courante. On va voir maintenant comment calculer efficacement ces quantités.

#### Récursions forward-backward

En utilisant les mêmes ressorts que précédemment, on peut montrer facilement que l'on a les relations suivantes

1.  ***Passe Forward :*** 

    $$\begin{aligned}
    \alpha_{n}(s) &=& \sum_{s'}{\gamma_n(s',s)\alpha_{n-1}(s')}
    \end{aligned}$$

    Le calcul de $\alpha_{n}(s)$ se réalise donc de manière récursive suivant les indices de temps croissants (Phase forward/aller). Le
    calcul se réalise sur les transitions possibles entre les états de départ $s_{n-1}$ et d'arrivée $s_n$.

2.  ***Passe Backward :*** 


    $$\begin{aligned}
    \beta_{n-1}(s') &=& \sum_{s}{\gamma_n(s',s)\beta_{n}(s)}
    \end{aligned}$$
    
    Le calcul de $\beta_{n}(s)$ se réalise donc de manière récursive suivant les indices de temps décroissants (Phase backward/retour).
    Le calcul se réalise sur les transitions possibles entre les états de départ $s_{n+1}$ et d'arrivée $s_{n}$.

#### Calcul des probabilités de transitions

Il ne reste plus qu'à calculer les propabiltés de transition. De manière directe, le calcul donne

$$\begin{aligned}
\gamma_n(s',s)&= p(s_n=s, y_n|s_{n-1}=s') \\
& =  p(y_n|s',s) . p(s|s')\\
\end{aligned}$$ 

avec

$$p(s|s')=\left \lbrace \begin{array}{cl} 0 &, \mbox{ si } \{s' \rightarrow s\} \mbox{ non valide}\\ \pi(u_n)&, \mbox{ sinon } \end{array}\right.$$

On peut alors écrire 

$$\begin{aligned}
\gamma_n(s',s)&=& p(y_n|c_n(s',s)) \pi(u_n) \mathbb{1}_{s' \rightarrow s} \nonumber \\
&=& \prod_{m=1}^{n_c}{p(y_n^{(m)}|c_n^{(m)(s',s)})} \pi(u_n) \mathbb{1}_{s' \rightarrow s}
\end{aligned}$$ 

avec $\pi(u_n)$ la probabilité à priori de $u_n$ et $c_n(s',s)$ les bits associés à l'étiquette $(s' \rightarrow s).$ La dernière inégalité est obtenue en considérant que le canal est un canal binaire sans mémoire.

Dans le cas où l'on considère une transmission codée sur un canal sans mémoire additif Gaussien, on a 

```{prf:example} Cas Gaussien

$$\forall n, \forall m \in \{1, \cdots, n_c \}, \;y_n^{(m)}=c_n^{(m)}+b_n^{(m)}, b_n^{(m)} \sim \mathcal{N}(0, \sigma_b^2)$$

$$\begin{aligned}
\Large \gamma_n(s',s)&=  \prod_{m=1}^{n_c}{p(y_n^{(m)}|c_n^{(m)}(s',s))} \nonumber \\
&=\frac{1}{\left(\sqrt{2 \pi \sigma_b^2} \right)^{n_c}} \exp{\left(-\frac{\sum_{m=1}^{n_c}{|y_n^{(m)}-c_n^{(m)}(s',s)|^2}}{2 \sigma_b^2}\right)} \pi(u_n) \mathbb{1}_{s' \rightarrow s} \nonumber
\end{aligned}$$
```

#### Initialisation des récursions forward-backward

Les phases forward backward nécessite une initialisation pour les états $\alpha_{0}(s)$ et $\beta_{L}(s)$. Cette initialisation dépend du type de fermeture appliquée au code convolutif.

1.  **Sans Fermeture de treillis :**

    Dans ce mode, on peut suppoeser le codeur initialisé dans l'état $s_0=0$. Seul un état est donc possible. Comme il n'y a pas de
    fermeture de treillis, tous les états finaux sont donc équi-probables. Dans ce cadre, il la mémoire du code est la mémoire
    du code $\nu$, on obtient alors

    $$\begin{aligned}
    \alpha_{0}(0) = 1 &,& \alpha_{0}(s) = 0 \; \mathrm{sinon} \nonumber\\
    &&\nonumber \\
    \beta_{L}(0) = 1/2^{\nu} &,& \forall s \nonumber
    \end{aligned}$$

2.  **Fermeture de treillis :**

    Dans ce cas, les états de départs et d'arrivée sont connus (on suppose qu'ils sont égaux à $s_0=0$).

    $$\begin{aligned}
    \alpha_{0}(0) = 1 &,& \alpha_{0}(s) = 0 \; \mathrm{sinon} \nonumber\\
    &&\nonumber \\
    \beta_{L}(0) = 1 &,& \beta_{L}(s) = 0 \; \mathrm{sinon} \nonumber
    \end{aligned}$$
    
#### Probabilité des états

On peut également accéder à la probabilité des états, relation utile dans certains (codeur à faible nombre d'état) car elle évite
l'utilisation d'un calcul directe de $p(s_{n-1}=s', s_{n}=s, { \bf y})$.
En effet, un calcul rapide permet d'écrire

$$\lambda_n(s)=p(s, {\bf y})=\alpha_{n}(s) \beta_n(s), \forall s,n$$

#### Résumé

L'algorithme complet peut alors être énoncé comme suit

```{prf:algorithm} Algorithme BCJR

1.  **Initialisation (avec fermeture treillis):** 

$$\begin{aligned}
    \alpha_{0}(0) = 1 &,& \alpha_{0}(s) = 0 \; \mathrm{sinon} \\
    \nonumber \\
    \beta_{L}(0) = 1 &,& \beta_{L}(s) = 0 \; \mathrm{sinon}
    \end{aligned}$$

2.  **Phase forward-backward :**

    $$\begin{aligned}
    \forall n=1, \cdots, L-1, \; \alpha_{n}(s) &=& \sum_{s'}{\gamma_n(s',s)\alpha_{n-1}(s')} \\
    \forall n=L-1, \cdots, 1, \;\beta_{n-1}(s') &=& \sum_{s}{\gamma_n(s',s)\beta_{n}(s)}
    \end{aligned}$$

3.  **Calcul de $L(u_n)$:** $\forall n=1, \cdots, K$

    $$\begin{aligned}
    L(u_n)&=&\log{\left[\frac{ \sum_{\mathcal{S}^{+}}{p(s_{n-1}=s', s_{n}=s, { \bf y})}}{\sum_{\mathcal{S}^{-}}{p(s_{n-1}=s', s_{n}=s, { \bf y})}}\right]}
    \end{aligned}$$
```


### Algorithme BCJR dans le domaine logarithmique

Pour des raisons pratiques, il est souvent plus comode d'exprimer l'algorithme BCJR dans le domaine logarithmique. Si on redéfinit les
équations précédentes en considérant le logarithme des quantités précédentes, on se retrouve à devoir dériver les récurrence pour les
nouvelles quantités données par

$$\tilde{\alpha}_n(s)\triangleq \log{(\alpha_n(s))}$$

$$\tilde{\beta}_{n}(s) \triangleq \log{(\beta_n(s))}$$

$$\tilde{\gamma}_n(s',s)\triangleq \log{(\gamma_n(s',s))}$$

#### Récursions dans le domaine logarithmique

En utilisant les définitions ci-dessus, après un change changement de variable, il vient 

$$\begin{aligned}
\tilde{\alpha}_n(s)&\triangleq& \log{(\alpha_n(s))} \nonumber \\
&=\log \sum_{s'}{\exp{(\tilde{\alpha}_{n-1}(s')+\tilde{\gamma}_n(s',s))}}  \nonumber\\
&  \nonumber \\
\tilde{\beta}_{n-1}(s')&\triangleq& \log{(\beta_n(s'))} \nonumber \\
&=\log \sum_{s}{\exp{(\tilde{\beta}_{n}(s)+\tilde{\gamma}_n(s',s))}} \nonumber\\\\
&  \nonumber
\end{aligned}$$

#### Calcul de $L(u_n)$

$$\begin{aligned}
L(u_n) = \log{(\sum_{\mathcal{S}^{+}}{\exp{(\tilde{\alpha}_{n-1}(s')+\tilde{\gamma}_n(s',s)+\tilde{\beta}_{n}(s))}})}-\log{(\sum_{\mathcal{S}^{-}}{\exp{(\tilde{\alpha}_{n-1}(s')+\tilde{\gamma}_n(s',s)+\tilde{\beta}_{n}(s))}})} \nonumber
\end{aligned}$$

#### L'opérateur $\max^*$

On définit ici un opérateur qui permettra de réécrire les équations précédentes et et d'en déduire des algorithmes faibles complexité. On
définit l'opérateur $\max^*{(x,y)}$ comme suit :

```{prf:definition} Opérateur $max^*$

$$\begin{aligned}
max^*{(x,y)}& \triangleq & \log{\left( e^x+e^y \right)} \nonumber\\
&=& \max{(x,y)} - \log{(1+e^{-|x-y|})} 
\end{aligned}$$
```
Cette définition dérive directement du fait que l'on peut écrire $\max{(x,y)}$ comme suit

$$\max{(x,y)} = \log{\left( \frac{e^x+e^y}{1+e^{-|x-y|}}\right)}$$

De la définition de l'opérateur, on peut déduire la propriété suivante :

```{prf:property}

$$\begin{aligned}
max^*{(x,y,z)}& \triangleq & \log{\left( e^x+e^y +e^z\right)} \nonumber\\
&=& \max^*(\max^*{(x,y)},z)
\end{aligned}$$

```

Cette expression se généralise à un nombre de termes quelconque.

#### Algorithme Log-MAP

A partir des expressions précédentes, on peut alors donner une version de l'agorithme MAP dans le domaine logarithmique.
```{prf:algorithm} Algorithme Log-MAP

1.  **Initialisation (avec fermeture treillis):** 

   $$\begin{aligned}
    \tilde{\alpha}_{0}(0) = 0 &,& \alpha_{0}(s) = - \infty \; \mathrm{sinon} \\
    \nonumber \\
    \beta_{L}(0) = 0 &,& \beta_{L}(s) = -\infty \; \mathrm{sinon}
    \end{aligned}$$

2.  **Phase forward-backward :**

    $$\begin{aligned}
    \forall n=1, \cdots, L-1, \; \tilde{\alpha}_n(s)&=& {\max_{s'}}^*{(\tilde{\alpha}_{n-1}(s')+\tilde{\gamma}_n(s',s))} \\
    \forall n=L-1, \cdots, 1, \; \tilde{\beta}_{n-1}(s')&=& {\max_{s}}^*{(\tilde{\beta}_{n}(s)+\tilde{\gamma}_n(s',s))}
    \end{aligned}$$

3.  **Calcul de $L(u_n)$:** $\forall n=1, \cdots, K$

    $$\begin{aligned}
    L(u_n) &=& {\max_{\mathcal{S}^{+}}}^*{\left(\tilde{\alpha}_{n-1}(s')+\tilde{\gamma}_n(s',s)+\tilde{\beta}_{n}(s)\right)} \nonumber \\ & &-{\max_{\mathcal{S}^{-}}}^*{\left(\tilde{\alpha}_{n-1}(s')+\tilde{\gamma}_n(s',s)+\tilde{\beta}_{n}(s)\right)}
    \end{aligned}$$

    où     $\max_{\mathcal{S}^{x}}^*{(.)}\triangleq \sum_{\mathcal{S}^{x}}{\exp{(.)}}$
```

D'un point de vue pratique, cette algorithme est implémenté d'une manière simplifié en utilisant l'opérateur $\max(.)$ et utilisation de
lookup table pour approximé le terme correctif.

#### Algorithme Max-Log-MAP

On peut réduire la complexité du Log-MaP en considérant le simple remplacement de l'opérateur ${\max}^*(.)$ par l'opérateur $\max(.)$. On néglige alors le terme correctif.

```{prf:algorithm} Algorithme Max-Log-MAP

1.  **Initialisation (avec fermeture treillis):** 

  $$\begin{aligned}
    \tilde{\alpha}_{0}(0) = 0 &,& \alpha_{0}(s) = - \infty \; \mathrm{sinon} \\
    \nonumber \\
    \beta_{L}(0) = 0 &,& \beta_{L}(s) = -\infty \; \mathrm{sinon}
    \end{aligned}$$

2.  **Phase forward-backward :**

    $$\begin{aligned}
    \forall n=1, \cdots, L-1, \; \tilde{\alpha}_n(s)&=& {\max_{s'}}{(\tilde{\alpha}_{n-1}(s')+\tilde{\gamma}_n(s',s))} \\
    \forall n=L-1, \cdots, 1, \; \tilde{\beta}_{n-1}(s')&=& {\max_{s}}{(\tilde{\beta}_{n}(s)+\tilde{\gamma}_n(s',s))}
    \end{aligned}$$

3.  **Calcul de $L(u_n)$:** $\forall n=1, \cdots, K$

    $$\begin{aligned}
    L(u_n) &=& {\max_{\mathcal{S}^{+}}}{\left(\tilde{\alpha}_{n-1}(s')+\tilde{\gamma}_n(s',s)+\tilde{\beta}_{n}(s)\right)} \nonumber \\ & &-{\max_{\mathcal{S}^{-}}}{\left(\tilde{\alpha}_{n-1}(s')+\tilde{\gamma}_n(s',s)+\tilde{\beta}_{n}(s)\right)}
    \end{aligned}$$
```
#### Log-MAP (log-BCJR) : cas Gaussien

Dans le cas Gaussien, on peut instancier la métrique de branche comme
suit :

$$\begin{aligned}
\tilde{\gamma}_n(s',s)&=\log{(\gamma_n(s',s))} \nonumber \\
&=\log(\pi(u_n))-n_c/2*\log{(2\pi \sigma^2)}-\frac{1}{2 \sigma^2} \sum_{m=1}^{n_c}{|y_n^{(m)}-c_n^{(m)}(s',s)|^2} \nonumber
\end{aligned}$$ 

en se réferant au critère MAP final, la constante peut-être supprimée.
