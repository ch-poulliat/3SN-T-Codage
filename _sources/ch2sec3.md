## Notions d'information souple

### Définition et propriétés

On définit la quantité suivante le log-rapport de probabilité ou log-likelihood (LLR) la quantité donnée par la définition suivante:


```{prf:definition} Log-likelihood ratio

$$\begin{aligned}
L(c_n)=\log{\left[\frac{p(c_n = 0 | { y_n})}{p(c_n = 1 | { y_n})}\right]}=\log{\left[\frac{p(c_n = 0 ; {y_n})}{p(c_n = 1 ; {y_n})}\right]}
\end{aligned}$$
```

Cette quantité est homogène à une information a posteriori. A partir de la relation précédente, on peut donner la relation suivante par simple
application de la règle de Bayes

$$L(c_n)=\log{\left[\frac{p({ y_n}|c_n = 0 )}{p( {y_n}|c_n = 1)}\right]}+\log{\left[\frac{p(c_n = 0 )}{p( c_n = 1)}\right]}=L_c(y_n)+L_a(c_n)$$

$L_c(y_n)$ est ce que l'on le log-rapport de vraisemblance qui est associé à la règle de décision ML dans le cas d'absence d'information a
priori sur le bit $c_n$ où dans le cas d'une source binaire i.i.d.. Le test est alors donné par

$$\begin{array}{ccc}
&\mathcal{H}_0 : c_n = 0 & \\
L_c(y_n)&\gtrless&0\\
&\mathcal{H}_1 : c_n = 1&
\end{array}$$ 


$|L_c(y_n)|$ représente la fiabilité de la décision associée au signe du LLR, qui donne lui la décision dure. $L_a(c_n)$ est
le LLR a priori associé au bit $c_n$. Le test 

$$\begin{array}{ccc}
& \mathcal{H}_0 : c_n = 0 & \\
L(c_n)&\gtrless&0\\
&\mathcal{H}_1 c_n = 1&
\end{array}$$ 

correspond donc au test MAP. La détection souple associée est donc donnée par : 

```{prf:definition} Détection souple d'un bit (MAP bit)
$$\begin{aligned}
\hat{c}_n &=& \mathrm{arg} \max_{c_n}{p(c_n | y_n) } \nonumber \\
&=& \frac{1-\mathrm{signe}(L(c_n))}{2}
\end{aligned}$$
```


On a les mêmes interprétations que pour $L_c(y_n)$ quant au module et au signe.

```{prf:example} Canal AWGN

Dans le cas du canal AWGN, on a 

$$y_n=x_n+b_n$$ 

où $x_n=1-2 c_n$ et $b_n$ un processus Gaussien centré de variance $\sigma_b^2$. Un calcul immédiat permet de d'avoir pour le cas d'une source binaire uniforme

$$L(c_n)=L_c(y_n)=\frac{2}{\sigma^2}y_n$$

L'application de la règle de décision ML/MAP dans ce cas donne

$$\begin{array}{ccc}
& \mathcal{H}_0 : c_n = 0 & \\
y_n&\gtrless&0\\
&\mathcal{H}_1 c_n = 1&
\end{array},$$ 

ce qui correspond à la règle de décision dure classique sur une modulation de type BPSK. On remarque que le LLR est une version pondérée de l'observation. Le facteur de pondération est proportionnel au rapport signal à bruit (exprimé en échelle linéaire). L'interprétation est la suivante: plus ce dernier est élevé, plus on donne de l'importance à ce que l'on observe, mais quand ce dernier tend vers $0$, on donne peu de crédit à cette dernière.

En développant l'expression du LLR qui est une fonction de l'observation, on en déduit que, conditionnellement au bit émis, ce dernier est une variable aléatoire telle que

$$L(c_n)\sim \mathcal{N}(m,2.|m|)$$ 

où 

$$m=\frac{2}{\sigma^2_b}x_n$$
```


```{prf:example} Canal de Rayleigh
Dans le cas du canal de Rayleigh parfaitement entrelacé et connaissance parfaite du canal, on a le modèle suivant 

$$y_n=\alpha_n x_n+b_n$$ 

où $x_n=1-2 c_n$, $b_n$ un processus Gaussien centré de variance $\sigma_b^2$ et $\alpha \sim \mathcal{R}(1/\sqrt(2))$ (loi de Rayleigh
normalisé, ie. $\boldsymbol{\mathbb{E}}(\alpha^2)=1)$. Un calcul immédiat permet de d'avoir pour le cas d'une source binaire uniforme

$$L(c_n)=\log{\left[\frac{p({ y_n}|c_n = 0;\alpha_n )}{p( {y_n}|c_n = 1;\alpha_n)}\right]}=\frac{2}{\sigma^2}\alpha_n y_n$$
```

On peut également noter que la connaissance du LLR permet de remonter facilement aux probabilité en remarquant que

$$\begin{aligned}
p(u_n =0 | { y_n}) + p(u_n =1 | { y_n})= 1 \\
\nonumber \\
L(u_n) = \log{\left(\frac{p(u_n = 0 | {y_n})}{p(u_n = 1 | { y_n})}\right)}
\end{aligned}$$

On obtient alors les relations suivantes

$$\begin{aligned}
p(u_n =0 | {y_n}) & = & \frac{e^{L(u_n)}}{1+e^{L(u_n)}} \\
\nonumber \\
p(u_n =1 | {y_n}) & = & \frac{1}{1+e^{L(u_n)} }
\end{aligned}$$

Ces expressions nous donnent alors le terme générique de cette probabilité a postériori donnée en fonction de $u_n$ par

$$p(u_n | {y_n})  =  \frac{e^{(1-u_n)L(u_n)}}{1+e^{L(u_n)}}$$

L'expression en fonction de $x_n=1-2.u_n$ s'obtient par multiplication au numérateur et dénominateur par $e^{-\frac{L(u_n)}{2}}$

$$p(u_n | {y_n})  =  \frac{e^{x_n\frac{L(u_n)}{2}}}{e^{-\frac{L(u_n)}{2}}+e^{+\frac{L(u_n)}{2}}}$$

### Interprétation du point de vue de la théorie de l'estimation

La quantité $L(u_n)$ est souvent appelée ***information souple***. En utilisant les expressions précédentes, elle peut être reliée à la quantité $\hat{x}_n=\boldsymbol{\mathbb{E}}(X_n|Y_n=y_n)$, quelquefois dénommée ***soft bits***, de la façon suivante:

$$\hat{x_n}=\boldsymbol{\mathbb{E}}(X_n|Y_n=y_n)=\tanh{\left(\frac{L(u_n)}{2}\right)}$$

On peut montrer que $\hat{x}_n$ est la meilleure estimée non linaire au sens du MMSE, ie.

$$\hat{x}(n)= \mathrm{arg} \min_{{x \in \mathbb{R}}}{\boldsymbol{\mathbb{E}}(|x(n)-\hat{x}(n)|^2)}$$

### Interprétation dans le domaine de Fourier

La transformée de Fourier d'une fonction ${f}$ définie sur $\mathbb{Z}_2$ munie des opérations usuelles (addition, multiplication) définies sur le corps binaire est donnée par

$$\mathbf{\hat{f}}=\mathbf{F}\mathbf{f}$$

$$\begin{pmatrix}
\hat{f}[0]\\
 \hat{f}[1] \\
 \end{pmatrix} = 
\begin{pmatrix}
 1 & 1 \\
 1 & -1  \\
 \end{pmatrix}\;\begin{pmatrix}
{f}[0]\\
{f}[1] \\
 \end{pmatrix}$$

L'application de cette transformation de Fourier à la fonction de $\mathbb{Z}_2$ dans $\mathbb{R}$ nous permet d'écrire 

$$\begin{pmatrix}
\hat{f}[0]\\
 \hat{f}[1] \\
 \end{pmatrix} = 
\begin{pmatrix}
 1 & 1 \\
 1 & -1  \\
 \end{pmatrix}\;\begin{pmatrix}
p(u_n=0|y_n)\\
p(u_n=1|y_n) \\
 \end{pmatrix},$$ 
 
 ce qui donne 
 
 $$\begin{pmatrix}
\hat{f}[0]\\
 \hat{f}[1] \\
 \end{pmatrix} = 
\begin{pmatrix}
 1 \\
 \tanh{\left(\frac{L(u_n)}{2}\right)}
 \end{pmatrix}.$$

On en déduit que l'estimée $\hat{x_n}$ se base sur un critère fréquentiel de détection.

### Estimation efficace de la capacité des canaux binaires

Si on considère le modèle discret équivalent suivant

$$y[n]=x[n]+b[n],$$ 

où $x[n] \in\{-1,+1\}$ et $b[n]$ suit une loi Gaussienne centrée de variance $\sigma_b^2;$ la formule de la capacité
gaussienne pour une entrée contrainte nous donne

$$I(X ; Y)=\frac{1}{2} \sum_{x=\pm 1} \int_{\mathbb{R}} f(y \mid x) \log _{2}\left(\frac{2 f(y \mid x)}{f(y \mid x=+1)+f(y \mid x=-1)}\right) d y.$$

En utilisant le fait que 

$$I(X ; Y)=H(X)-H(X \mid Y),$$ 

on peut écrire

$$I(X ; Y)=1+\mathbb{E}_{X, Y}\left(\log _{2}(p(X \mid Y))\right)$$ 

En introduisant l'expression du LLR (dont la dépendance explicite à l'observation est appuyée par la notation choisie dans cette section)

$$L(y)=\log \left(\frac{p(x=+1 \mid Y=y)}{p(x=-1 \mid Y=y)}\right),$$ 

en utilisant le fait que $p(x=+1 \mid y)+p(x=-1 \mid y)=1, \; \forall y,$ il vient 

$$\begin{aligned}
p(x=+1 \mid y) &=\frac{e^{L(y)}}{1+e^{L(y)}} \\
&=\frac{1}{1+e^{-L(y)}} \\
p(x=-1 \mid y) &=\frac{1}{1+e^{L(y)}}
\end{aligned}$$ 

Ce qui permet d'écrire, l'expression générique en $x$

$$p(x \mid y)=\frac{1}{1+e^{-x L(y)}}.$$ 

Par intégration de Monte-Carlo, on obtient alors un estimateur empirique non biaisé simple donné par

$$\hat{I}(X ; Y)=1+\frac{1}{N} \sum_{n=0}^{N-1} \log _{2}(p(x[n] \mid y[n]))=1-\frac{1}{N} \sum_{n=0}^{N-1} \log _{2}\left(1+e^{-x[n] L(y \mid n])}\right).$$

### Estimation ML séquence basée sur les LLR.

On également redériver le critère ML en fonction du LLR En supposant, le canal sans mémoire et en repartant de l'expression

$$p({\bf y} | {\bf c})=p({\bf y} | {\bf x})=\prod_n^{N-1}{p(y(n)|x(n))}$$

et en utilisant le fait que

$$L(c_n)=\log{\left[\frac{p({ y_n}|c_n = 0)}{p( {y_n}|c_n = 1)}\right]},$$

on peut alors par changement de variable redonner l'expression du critère ML de la façon suivante:

$$\begin{aligned}
{\bf c}&=\mathrm{arg} \max_{{\bf c'}}{p({\bf y} | {\bf c'})} \nonumber \\
&=\mathrm{arg} \max_{{\bf c'=\mathcal{M}^{-1}(x)}}{\prod_n^{N-1}{\frac{e^{x_n\frac{L(c'_n)}{2}}}{e^{-\frac{L(c'_n)}{2}}+e^{+\frac{L(c'_n)}{2}}}}} \nonumber \\
&=\mathrm{arg} \max_{{\bf c'=\mathcal{M}^{-1}(x)}}{\sum_n x_n L(c'_n)} \nonumber \\
&=\mathrm{arg} \max_{{\bf c'=\mathcal{M}^{-1}(x)}}{\sum_n (1-2 c_n) L(c'_n)} 
\label{eqn:demin}
\end{aligned}$$

On remarque alors que pour chaque mot de code on réalise une *corrélation* entre le mot reçu (ou de manière équivalent la séquence de LLR associée) et un mot de code valide. Ainsi, la dernière expression permet de donner la structure brute d'un décodeur ML : on peut l'assimiler à un banc de corrélateurs dont chacune des $2^K$ branche est la corrélation avec un mot de code possible. Pour la décision il suffit alors de sélectionner la branche dont la sortie est la plus grande. D'un point de vue complexité, l'approche brute force est de $2^K N=2^{R\;N} N$ multiplications et $2^{R\;N} (N-1)$ additions. On a donc une complexité exponentielle en la taille du mot de code. Pour chaque famille de code, on cherchera à utiiser la structure propre du code pour "casser" cette complexité.

On discute maintenant de quelques cas simples.

```{prf:example} Code à répétitions
Pour un code de répétition de taille $N$, de rendement $R=1/N$, on a deux mots de codes le mot de codes ${\bf c_0}=[0 \cdots 0]$ et ${\bf c_1}=[1 \cdots 1]$, tous les deux dans $\mathbb{F}_2^N$. Sélectionner le mot de code le plus probable revient à réaliser le test suivant

$$\begin{array}{ccc}
&\mathcal{H}_0 : {\bf c_0} & \\
\sum_{n=0}^{N-1} L(c_n)&\gtrless&0\\
&\mathcal{H}_1 : {\bf c_1}&
\end{array}$$

Ce test permet également de déterminer le bit d'information émis :

$$\begin{array}{ccc}
&\mathcal{H}_0 : u=0 & \\
\sum_{n=0}^{N-1} L(c_n)&\gtrless&0\\
&\mathcal{H}_1 : u=1&
\end{array}$$
```

```{prf:example} Code de parité
Pour un code de répétition de taille $N$, de rendement $R=(N-1)/N$, on a $2^{N-1}$ mots de codes, tous dans $\mathbb{F}_2^N$. Si on prend une approche *"brute-force"* non structurée, ie. purement énumérative, sélectionner le mot de code le plus probable revient à réaliser un *"banc de filtre" ou "de corrélations"* du vecteur des LLRs reçus avec l'ensemble des mots de codes possibles. Cela revient à un test à $2^{N-1}$ hypothèses . On voit bien que sans prendre en compte la structure de ce code, l'énumération devient prohibitive quand $N$ croit.
```
