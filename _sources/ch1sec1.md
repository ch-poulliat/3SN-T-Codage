## Mesure de l'information : notion d'entropie

### Information propre 

Soit $X$ une variable aléatoire discrète et $X=x$ un événement de
probabilité $p(x)$, une mesure de l'information, notons-là $h(x),$
s'identifie à une mesure de l'inattendu, de l'improbable. Ainsi, une
information apportée par la réalisation de l'événement $X$ sera d'autant
plus importante que celle-ci est peu probable, ie.

$$h(x)=f\left(\frac{1}{p(x)}\right).$$ 

Concernant la notion d'information, les propriétés attendues sont:

1.  $f(.)$ est une fonctionnelle croissante de $p(x),$

2.  $f(p)=0$ quand $p \rightarrow 1$ (événement certain)

3.  $f(p \cdot q)=f(p)+f(q)$ (additivité de l'information pour des
    événements indépendants $: h(x$ et $y)=h(x)+h(y)).$

Compte tenu de cette axiomatique, la fonction $f(p)=-\log (p)$ est la seule fonction qui soit à la fois positive, continue sur $[0,1)$ et qui vérifie l'additivité des informations indépendantes. La base du logarithme est elle indifférente.

```{prf:definition} Information propre
Soit $X$ une variable aléatoire discrète et $X=x$ un événement de probabilité $p(x)$, on appelle information propre ou quantité
d'information apportée par l'événement $x$, la quantité

$$h(x)=\log \left(\frac{1}{p(x)}\right)=-\log (p(x))$$
```

```{prf:property}
1.  positivité :

    $$ h(x) \geq 0$$

2.  additivité : soient $x$ et $y$ deux événements indépendants, alors

    $$h(x \text { et } y)=h(x)+h(y)$$

```

Quand le la base du logarithme est la base naturel $(\log_e(.))$, on parle de Shannon (Sh.) ou d'unité naturelle, notée *nats* pour *natural units*. Si on utilise un logarithm en base $2$ $(\log_2(.)),$ on parle d'unité binaire, notée *bits* pour *binary units*. Ainsi, pour une source binaire à valeur dans $\{0,1\}$ equi-distribuée de symbolesindépendants, l'information propre associée à chaque symbole binaire est $h(1 / 2)=1$ bits. Pour une source $M$ -aire à valeur dans $\{0,1 \cdots, M-1\}$ equidistribuée de symboles indépendants, l'information propre associée à chaque symbole est $h(1 / M)=\log _{2}(M)$ bits.

### Entropie associée à une variable aléatoire discrète

```{prf:definition} Entropie

Soit $\mathbf{X}$ une variable aléatoire discrète à valeurs dans l'alphabet $\mathcal{X}$ de d.d.p. $p(x)=Prob(X=x), \; x \in \mathcal{X}$, alors l'entropie associée est donnée par

$$\begin{aligned}
\boldsymbol{\mathbf{H}}(X)&= -\sum_{x \in \mathcal{X}}{p(X=x)\log_2{(p(X=x))}} \nonumber \\
&= - \boldsymbol{\mathbb{E}}(\log_2{p(X)})
\end{aligned}$$
```


C'est la *"quantité d'information moyenne"* exprimée en bits/symbole.

```{prf:property}

-   $\boldsymbol{\mathbf{H}}(X)$ est déterministe et c'est une
    fonction(nelle) de $p(x)$,

-   $\boldsymbol{\mathbf{H}}(X) \geq 0$ (positivité),

-   $\boldsymbol{\mathbf{H}}(X)=0$ $\Leftrightarrow$ $X$ est
    déterministe,

-   $\boldsymbol{\mathbf{H}}(X)=\log_2{(M)}$ pour distribution uniforme
    de symboles $M$-aire,

-   Invariance par équivalence (ie. $Y=f(X)$ où $f(.)$ inversible),

-   L'entropie d'une source $M$-aire vérifie

    $$\boldsymbol{\mathbf{H}}(X) \leq \log_2{(M)}$$ 
    
    avec égalité pour une source à distribution uniforme.

```
```{prf:example}
Soit $X$ à valeurs dans un alphabet binaire $\mathcal{X}=\left\{x_{0}, x_{1}\right\}$ tel que $P\left(X=x_{0}\right)=p$ and
$P\left(X=x_{1}\right)=1-p.$ Alors

$$\mathrm{H}(X)=\mathrm{H}_{\mathrm{b}}(p)$$ 

où $\mathrm{H}_{\mathrm{b}}(\mathrm{p})$ est ce que l'on nomme la fonction d'entropie binaire donnée par

$$\mathrm{H}_{\mathrm{b}}(p) \triangleq p \log \frac{1}{p}+(1-p) \log \frac{1}{1-p}$$
```

### Entropie conjointe et conditionnelle

```{prf:definition} Entropie conjointe 

Soient $X$ et $Y$ deux variables aléatoires discrètes

$$\begin{aligned}
\boldsymbol{\mathbf{H}}(X,Y)&= \nonumber -\sum_{x \in \mathcal{X}} \sum_{y \in \mathcal{Y}}{p(X=x,Y=y)\log_2{(p(X=x, Y=y))}}\\
&=  - \boldsymbol{\mathbb{E}}(\log_2{p(X,Y)})
\end{aligned}$$
```

On remarquera que

$$\boldsymbol{\mathbf{H}}(X,Y)=\boldsymbol{\mathbf{H}}(Y,X).$$

```{prf:definition} Entropie de $Y$ sachant $X=x$

soient $X$ et $Y$ deux variables aléatoires discrètes, alors l'entropie de $Y$ sachant $X=x$ est donnée 

$$\begin{aligned}
\boldsymbol{\mathbf{H}}(Y|X=x)&= -\sum_{y \in \mathcal{Y}}{p(Y=y|X=x)\log_2{(p(Y=y |X=x))}} \nonumber\\
&=  - \boldsymbol{\mathbb{E}}(\log_2{p(Y | X=x)})
\end{aligned}$$
```

```{prf:definition} Entropie conditionnelle
$$\begin{aligned}
\boldsymbol{\mathbf{H}}(Y|X)&= -\sum_{x \in \mathcal{X}} \sum_{y \in \mathcal{Y}}{p(X=x,Y=y)\log_2{(p(Y=y |X=x))}} \nonumber\\
&= \sum_{x \in \mathcal{X}}p(X=x)\boldsymbol{\mathbf{H}}(Y|X=x) = \boldsymbol{\mathbb{E}}(\boldsymbol{\mathbf{H}}(Y|X=x))\nonumber\\
&=  - \boldsymbol{\mathbb{E}}(\log_2{p(Y | X)})
\end{aligned}$$
```

```{prf:property}
1.  **chain rule :**

    $$\boldsymbol{\mathbf{H}}(X,Y) = \boldsymbol{\mathbf{H}}(X) + \boldsymbol{\mathbf{H}}(Y|X)=\boldsymbol{\mathbf{H}}(Y) + \boldsymbol{\mathbf{H}}(X|Y)$$


2.  **borne inf :**

    $$\boldsymbol{\mathbf{H}}(X,Y) \geq \boldsymbol{\mathbf{H}}(X) \mbox{ ou } \boldsymbol{\mathbf{H}}(Y)$$

3.  **Conditionnement :**

    $$\boldsymbol{\mathbf{H}}(X|Y) \leq \boldsymbol{\mathbf{H}}(X)$$

    égalité si $X$ et $Y$ indépendants

4.  **Décroissance par conditionnement :**

    $$\boldsymbol{\mathbf{H}}(X_1|X_2,\cdots,X_n) \leq \cdots \leq \boldsymbol{\mathbf{H}}(X_1|X_2,X_3) \leq \boldsymbol{\mathbf{H}}(X_1|X_2) \leq\boldsymbol{\mathbf{H}}(X_1)$$

5.  **Encadrement (sous additivité de l'entropie) :**

    $$\boldsymbol{\mathbf{H}}(X,Y) \leq \boldsymbol{\mathbf{H}}(X)+\boldsymbol{\mathbf{H}}(Y) \leq 2 \boldsymbol{\mathbf{H}}(X,Y)$$

6.  **Entropie conjointe et conditionnement :**

    $$\boldsymbol{\mathbf{H}}(X,Y|Z)=\boldsymbol{\mathbf{H}}(X|Z)+\boldsymbol{\mathbf{H}}(Y|X,Z)$$

7.  **positivité :** 

    $$\boldsymbol{\mathbf{H}}(X|Y) \geq 0$$

    égalité si $X=f(Y)$ où $f(.)$ déterministe
```


L'ensemble des définition précédentes se généralise assez facilement au cas de vecteurs de dimension supérieure à $2.$ En particulier, soit
$X_1, X_2,\cdots X_n$ de loi conjointe $p(x_1,x_2,\cdots,x_n),$ on aura par définition

$$\boldsymbol{\mathbf{H}}(X_1, X_2,\cdots X_n)=-\boldsymbol{\mathbb{E}}(log_2(p(X_1, X_2,\cdots X_n))).$$

On peut vérifier que

$$\boldsymbol{\mathbf{H}}(X_1, X_2,\cdots X_n) \leq \sum_{i=1}^n{\boldsymbol{\mathbf{H}}(X_i)},$$

avec égalité si et seulement si les $X_i$ sont indépendants. La relation chaînée associée à l'entropie est quant à elle donnée par

$$\boldsymbol{\mathbf{H}}(X_1, X_2,\cdots X_n)=\sum_{i=1}^n{\boldsymbol{\mathbf{H}}(X_i|X_{i-1},\cdots X_1)}.$$

### Entropie(s) associée(s) à une variable aléatoire continue

Si la notion d'information est bien reliée à l'entropie d'une variable aléatoire discrète, ce lien est moins évident pour une variable
aléatoire continue. 

```{prf:definition} Entropie différentielle
Soit $X$ une variable aléatoire continue définie par une densité de probabilité $f(x),$ alors l'entropie différentielle est donnée

$$h(X)=-\int f(x) \log _{2}(f(x)) d x$$
```
On ne peut pas interpréter $h(X)$ comme une mesure d'information ou d'incertitude dans le cas continue. Ceci peut se voir dans le cas d'un
changement de variable. Soit $Y=f(X),$ par changement de variable, on a $h(X) \neq h(Y)=h(f(X))$ donc $h(X)$ n'est pas une mesure d'information
stricte. Dans le cas particulier du changement d'échelle, tel que $Y=a X,$ on a $h(X) \neq h(a X)=h(X)+\log (a)$ qui peut même être négatif!

```{prf:property}
1.  Loi uniforme sur $[a, b]:$ 

    $$\begin{array}{c}
    f(x)=\frac{1}{b-a} \\
    h(x)=\log (b-a)
    \end{array}$$

2.  Loi normale de moyenne $\mu$ et variance $\sigma^{2}:$

    $$f(x)=\frac{1}{\sqrt{2 \pi \sigma^{2}}} \exp \left(-\frac{(x-\mu)^{2}}{2 \sigma^{2}}\right)$$

    $$h(x)=\frac{1}{2} \log 2 \pi e+\log (\sigma)$$
```

Comme pour le cas discret, on peut définir des entropies conjointes et conditionnelles. Soit $X_{1}, X_{2}, \cdots, X_{n}$ associées à la
densité conjointe $f\left(x_{1}, x_{2}, \cdots, x_{n}\right),$ l'entropie différentielle conjointe est définie comme suit

$$h\left(X_{1}, X_{2}, \cdots, X_{n}\right)=-\int f\left(x_{1}, x_{2}, \cdots, x_{n}\right) \log _{2}\left(f\left(x_{1}, x_{2}, \cdots, x_{n}\right)\right) d x_{1} d x_{2} \cdots d x_{n}.$$

De même pour deux v.a. $X$ et $Y$, l'entropie différentielle conditionnelle de $X$ sachant $Y$ est donnée par

$${h}(X \mid Y)=-\int f(x, y) \log _{2}(f(x \mid y)) d x d y.$$

Ces quantités sont très utiles car elles permettent de calculer l'information mutuelle entre deux variables aléatoires, quantité fondamentale en théorie de l'information et qui pour le coup à la même interprétation en discret et en continu.

