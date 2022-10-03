## Critères de décodage séquence

### Décodage MAP/ML séquence
```{prf:definition} Décodage par maximum a posteriori séquence

$$\begin{aligned}
\hat{{\bf c}}&=& \mathrm{arg} \max_{{\bf c'}}{p({\bf c'} | {\bf y}) } \nonumber\\
& =& \mathrm{arg} \max_{{\bf c'}}{\frac{p({\bf y} | {\bf c'})p({\bf c'})}{p({\bf y})}}\nonumber\\
& =& \mathrm{arg} \max_{{\bf c'}}{p({\bf y} | {\bf c'})p({\bf c'})}
\end{aligned}$$
```
```{prf:definition} Décodage par maximum de vraisemblance séquence

$$\begin{aligned}
\hat{{\bf c}}&=& \mathrm{arg} \max_{{\bf c'}}{p({\bf y} | {\bf c'})}
\end{aligned}$$
```

Dans le cas où l'on considère l'ensemble des mots de codes équiprobable ($p({\bf c})=1/2^K$), les critères MAP et ML séquence sont équivalents.
En pratique, le critère minimisé est équivalent à la minimisant d'un taux d'erreur trame (Frame Error Rate, FER) et non à la minimisaton d'un
taux d'erreur binaire (Bit Error Rate, BER).

### Exemples de canaux.

On peut alors spécifier ces critères en fonction du canal considéré. Deux types de canaux rencontrés régulièrement sont le canal à erreur
binaire symétrique (BSC) et le canal à bruit blanc additif Gaussien (AWGN).

```{prf:example} Canal binaire symétrique (BSC)

::: center
![Représentation d'un canal de type BSC](./BSC.jpg){#fig:ch1_BSC
width="60%"}

[]{#fig:ch1_BSC label="fig:ch1_BSC"}
:::

Pour ce canal représenté figure [2.1](#fig:ch1_BSC){reference-type="ref" reference="fig:ch1_BSC"}, le mot reçu est modélisé par le signal émis et
une erreur binaire :

$$\forall n=0, \cdots N-1, y(n)=c(n)\oplus e(n)$$ 

où $e(n) \in\{0,1\}$ sont des v.a. i.i.d. binaires telles que $p(e(n)=1)=p$, indépendantes de $c(n)$. $\oplus$ est l'addition modulo-2 (équivalent à l'opération
OU-Exclusif/XOR).

Le canal étant sans mémoire, on a donc

$$p({\bf y} | {\bf c})=p({\bf e})=\prod_n^{N-1}{p(e(n))}=\prod_n^{N-1}{p(y(n)|c(n))}$$

ce qui équivaux à

$$p({\bf y} | {\bf c}))= (1-p)^{N-d_H({\bf y},{\bf c})}p^{d_H({\bf y},{\bf c})}$$

soit

$$\begin{aligned}
\log{\left( p({\bf y} | {\bf c}))\right)}&=N \log{(1-p)}-d_H({\bf y},{\bf c}) \log(1-p)+ d_H({\bf y},{\bf c}) \log(p) \nonumber\\
&=N \log{(1-p)}+d_H({\bf y},{\bf c}) \log{\left( \frac{p}{(1-p)}\right)}
\end{aligned}$$ 


comme $p \leq 0.5$, on a $\log{\left(p/(1-p)\right)}<0$, d'où l résultat suivant: 

$$\begin{aligned}
{\bf c}&=\mathrm{arg} \max_{{\bf c'}}{p({\bf y} | {\bf c'})} \nonumber \\
&=\mathrm{arg} \max_{{\bf c'}}{\log{(p({\bf y} | {\bf c'}))}} \nonumber\\
&=\mathrm{arg} \min_{{\bf c'}}{d_H({\bf y},{\bf c'})} 
\end{aligned}$$

***Sur canal binaire symétrique (détection à décisions "dures" (hard decoding/decision)), le mot de code le plus probable est donc celui qui minimise la distance au sens de Hamming avec le mot reçu.***
```
```{prf:example} Canal additif blanc Gaussien à entrées binaires/antipodales

Sur canal Gaussien, le modèle échantillonné est donné par

$$\forall n=0\cdots N-1, y(n)=x(n)+b(n)$$

où $x(n) \in \{+1,-1\}$ est la version modulée en BPSK des bits codés $c(n) \in \{0,1\}$ tels que $x(n)=\mathcal{M}(c(n))=1-2c(n)=(-1)^{c(n)}$, soit le mapping $\{'0' \leftrightarrow '+1', '1' \leftrightarrow '-1'\}$. ${b(n)}_{n=0 \cdots N-1}$ est un processus aléatoire Gaussien où $b(n)$ sont des v.a. Gaussiennes réelles i.i.d de densité de probabilité $\mathcal{N}(0, \sigma_b^2)$.

Le canal étant sans mémoire, on a donc

$$p({\bf y} | {\bf c})=p({\bf y} | {\bf x})=\prod_n^{N-1}{p(y(n)|x(n))}$$

ce qui équivaut à

$$p({\bf y} | {\bf x})\propto \prod_n{e^{-\frac{(y(n)-x(n))^2}{2 \sigma_b^2}}}$$

En prenant le $\log$, on obtient alors facilement, 

$$\begin{aligned}
{\bf c}&=\mathrm{arg} \max_{{\bf c'}}{p({\bf y} | {\bf c'})} \nonumber \\
&=\mathrm{arg} \max_{{\bf c'}}{\log{(p({\bf y} | {\bf c'})}} \nonumber \\
&= \mathrm{arg} \min_{{\bf c'=\mathcal{M}^{-1}(x'(n))}}{\sum_n{(y_n-x_n')^2}} 
\label{eqn:demin}
\end{aligned}$$

où $d_E({\bf y},{\bf c'})=\sum_n{(y_n-c_n')^2}$ représente la distance Euclidienne entre les deux séquences de bits codés émises. Donc sur canal AWGN, le mot de code le plus probable est celui qui est le plus proche de la séquence reçue au sens de la distance euclidienne.

On peut aller plus loin sur la simplification de l'expression  précédente. En effet, en développant on obtient

$$\begin{aligned}
\sum_n{(y_n-x_n)^2}&=& \sum_n{y_n^2}-2\sum_n{y_n x_n}+\sum_n{x_n^2} \nonumber
\end{aligned}$$

Comme le premier et troisième ($x_n^2=1$) termes du membre de droite sont les mêmes pour tout mot de code, en prenant le $\log$, on obtient alors facilement, 

$$\begin{aligned}
{\bf c}&= &\mathrm{arg} \max_{{\bf c'=\mathcal{M}^{-1}(x'(n))}}{\sum_n{y_n x_n'}} 
\label{eqn:intercorrdecodage}
\end{aligned}$$

On interprète ici comme la recherche de l'intercorrélation maximale entre le signal reçu et le signal émis. On peut encore le réécrire en
fonction de $c(n)$ comme suit 

$$\begin{aligned}
{\bf c}&= &\mathrm{arg} \min_{{\bf c'}}{\sum_n{y_n c_n'}} \nonumber \\
&=&\mathrm{arg} \min_{{\bf c'}}{\sum_{n|c'_n=1}{y_n}} 
\label{eqn:intercorrdecodagev2}
\end{aligned}$$

On verra par la suite que l'on peut avoir également une interprétation dans le cadre d'un décodage "souple".
```