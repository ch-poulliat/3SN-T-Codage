## Capacité d'un canal de transmission

### Définition

Soit $X \in \mathcal{X}$ le symbole émis et $Y \in \mathcal{Y}$, la sortie observée du canal de transmission supposé sans mémoire
caractérisé par la probabilité de transition $P(Y|X)$ alors on à la définition suivante 


```{prf:definition} Capacité d'un canal discret sans mémoire
La capacité d'un canal sans mémoire est donnée par 

$$\begin{aligned}
\mathbf{C} & =  \max_{p(X)}{\boldsymbol{\mathbf{I}}(X;Y)} \\
& =  \max_{p(X)}{\boldsymbol{\mathbf{H}}(X) -\boldsymbol{\mathbf{H}}(X|Y)} = \max_{p(X)}{\boldsymbol{\mathbf{H}}(Y) -\boldsymbol{\mathbf{H}}(Y|X)} \nonumber
\end{aligned}$$

Max. atteint pour distribution uniforme pour les canaux *symétriques*.
```


Cette quantité représente le débit maximum atteignable avec un probabilité arbitrairement faible par un canal de transmission donné par $P(Y|X).$ Il est mesuré en bit par symbole, souvent noté bpcu (bit per channel use).

### Exemples de canaux à entrées et sorties discrètes sans mémoire

```{prf:example}  Canal à effacement 

Le canal à effacement (binary erausre channel, BEC) est un exemple simple de canaux sans mémoire à entrée binaire et sortie ternaire. c'est
une modélisation simple d'un canal de type *"internet"* (effacement des paquet à l'aide de CRC quand intégrité du paquet n'est pas assurée).
Ainsi chaque bit $X$ émis $'0'$ ou $'1'$ est soit reçu sans erreur avec ne probabilité $1-\epsilon$ ou considéré comme effacé, noté $E$, avec
une probabilité $\epsilon.$ On peut alors montrer que la capacité de cecanal se résume à 

$$C_{\mathrm{BEC}}=1-\epsilon.$$

```


```{prf:example} Canal binaire symétrique

Le canal binaire symétrique à erreurs (binary symetric channel, BSC) est un canal qui modélise les erreurs dans le domaine décidé, et donc sous
décision dure au récepteur (hard decision). Dans ce cas, le bit $X$ est reçu coorectement avec un probabilité $1-p$ ou erroné avec une probabilité $p$, où $p$ est a probabilité d'erreur bit ou *"taux de flip"* Dan ce cas la capacité est donnée par

$$C_{\mathrm{BSC}}=1-\mathrm{H}_{\mathrm{b}}(p)$$

```

### Exemples de Canaux à entrées continues et sorties continues

Pour des entrées et sorties à densités continues, l'expression générale de l'information mutuelle est donnée par

$$I(X ; Y)=\int p(x, y) \log \frac{p(x, y)}{p(x) p(y)} d x d y.$$

La capacité est alors obtenue pour un canal donné par maximisation sur la densité de la variable en entrée de canal. Parmi les canaux
d'intérêt, on a le canal Gaussien à temps continu qui est un des cas de canal continu adressé par Shannon à l'origine. Dans ce modèle, le
signal observé $y(t)$ est une version bruité du signal envoyé $x(t)$ est un signal de puissance $P$ et à bande limitée $W=1/T,$ où $T$ est le
temps symbole. Le modèle continue est alors le suivant

$$y(t)=x(t)+b(t).$$

où $b(t)$ est un processus Gaussien complexe de densité spectrale bilatérale de bruit $N_0.$ On définit alors le rapport signal-sur-bruit par 

$$\mathrm{SNR} \triangleq \frac{P}{\mathrm{N}_{0} W}.$$ 

On peut alors donner la capacité associée à ce canal par la proposition suivante (preuve admise). 

```{prf:definition} Capacité d'un canal Gaussien à temps continu
La capacité d'un canal Gaussien à temps continu et bande limitée $W$ est
donnée par

$$\mathrm{C}_{\mathrm{AWGN}-\mathrm{C}}=W \log_2 (1+\mathrm{SNR})[\mathrm{bits} / \mathrm{s}]$$

où 

$$\mathrm{SNR} \triangleq \frac{P}{\mathrm{N}_{0} W}.$$ 

$P$ est la puissance d'émission de $X$ et $N_0$ est la densité spectrale bilatérale du bruit. La capacité est atteinte pour une distribution Gaussienne de
l'entrée $X.$
```

Un modèle plus simple a abordé mais cependant équivalent sous certaines conditions est le modèle du canal Gaussien à temps discret. Celui-ci
correspond à une version discrétisée du canal précédent. Ainsi, on obtient le modèle discret suivant, ie. pour tout instant symbole $n,$ on
a 

$$y[n]=x[n]+b[n],$$ 

où $b[n]$ suit une loi normal complexe circulaire, $\mathcal{CN}(0,N_0).$ La loi de transition du canal s'écrit alors

$$p(y|x) \propto e^{-\frac{\vert y-x \vert^2}{N_0}}.$$ 


On peut alors démontrer la proposition suivante: 

```{prf:definition} Capacité d'un canal Gaussien à temps discret
La capacité d'un canal Gaussien à temps discret réel avec une énergie moyenne par symbole $\mathrm{E}_{\mathrm{s}}$ et une variance par
dimension $\sigma^{2}=\mathrm{No} / 2$ est donnée par

$$C_{\text {AWGN}}=\frac{1}{2} \log \left(1+\frac{E_{s}}{\sigma^{2}}\right) \text { [bits/channel use] or [bits/symbol], }$$

Cette capacité est atteinte pour $X \sim \mathcal{N}\left(0, \mathrm{E}_{\mathrm{s}}\right).$

Pareillement, La capacité d'un canal Gaussien complexe à temps discret avec une énergie moyenne par symbole $\mathrm{E}_{\mathrm{s}}$ et une
variance par dimension $\sigma^{2}=\mathrm{No} / 2$ est donnée par 

$$C_{AWGN}=\log \left(1+\frac{E_{s}}{2 \sigma^{2}}\right)=\log \left(1+\frac{E_{s}}{N_0}\right) \text { [bits/channel use] or [bits/symbol], }$$
```
La partie *"difficile"* de la preuve (non détaillée ici) reste de montrer que le maximum est atteint pour une distribution gaussienne. Une
fois ceci établi, la preuve fait appel aux expressions simples de l'entropie de variables aléatoires gaussiennes.

En remarquant que $W=1/T,$ on obtient $P=\mathrm{E}_{\mathrm{s}} W.$ Le lien entre les deux régimes est alors donné par la relation suivante :

$$\mathrm{C}_{\mathrm{AWGN}-\mathrm{C}}=W * C_{AWGN}.$$ 

On remarque alors que $\mathrm{C}_{\mathrm{AWGN}-\mathrm{C}}$ est homogène à un débit alors que $\mathrm{C}_{\mathrm{AWGN}}$ est homogène à une
efficacité spectrale en $bit/s/Hz.$

Pour les $E_s/N_0$ faibles (régime limité en puissance), on a

$$\begin{aligned}
\mathrm{C}_{\textrm{AWGN }} &=\log_2(1+E_s/N_0) \\
&\approx \frac{1}{\ln 2} \cdot E_s/N_0.
\end{aligned}$$ 

On a donc un régime linéaire. A contrario, pour les forts $E_s/N_0,$ on a un régime logarithmique, ie.
$$\mathrm{C}_{\textrm{AWGN }} \approx \log_2(E_s/N_0)$$

### Canaux à entrées discrètes et sorties continues

#### Capacité à entrées contraintes 

On considère maintenant des canaux à entrées discrètes. Ceci représente le cas d'usage le plus fréquent en communications numériques où les
symboles émis appartiennent à des constellations à des alphabets finis comme les modulations de type PAM, QAM ou encore PSK/APSK. Dans ce cas,
l'information mutuelle s'écrit comme suit

$$\mathrm{I}(X ; Y)=\sum_{x \in \mathcal{X}} \int p(x, y) \log_2 \frac{p(x, y)}{p(x) p(y)} d y,$$

avec $p(x,y)=p(y|x)p(x)$ et $p(y)=\sum_x p(y|x) p(x).$

La capacité associée à ce type d'entrées en souvent appelée ***capacité à entrées contraintes (constrained input capacity)***.  Si on considère des entrées contraintes avec une distribution uniforme des symboles d'entrée, avec $|\mathcal{X}|=M,$ on aura $p(x)=1/M, \forall x \in \mathcal{X},$ et on a donc l'expression suivante

$$\mathbf{C}=\mathrm{I}(X ; Y)=\frac{1}{M}\sum_{x \in\mathcal{X}}\int p(y|x) \log_2 \frac{p(y|x)}{\frac{1}{M} \sum_x p(y|x)} dy.$$

### Calcul numérique de la capacité 

Contrairement au cas Gaussien à entrées continues, il n'existe pas d'expression analytique plus simple que cette formulation intégrale. Il faut donc pour un canal particulier calculer l'expression intégrale par *intégration numérique* ou de *Monte-Carlo*. Calculer la capacité revient à évaluer

$$\mathbf{C} = \boldsymbol{\mathbf{I}}(X;Y) = \boldsymbol{\mathbf{H}}(X)-\boldsymbol{\mathbf{H}}(X|Y)$$

au travers des Termes $\boldsymbol{\mathbf{H}}(X)$ et $\boldsymbol{\mathbf{H}}(X|Y).$ 

Voilà alors les différentes étapes pour calculer la capacité "numériquement" :

-   ***Calcul de $\boldsymbol{\mathbf{H}}(X)$ :***

    En considérant une distribution  uniforme des symboles d'entrée, on obtient facilement que
    
    $$\boldsymbol{\mathbf{H}}(X)=\log_2(M).$$

-   ***Calcul de $\boldsymbol{\mathbf{H}}(X|Y)$ :***

    $$\boldsymbol{\mathbf{H}}(X|Y)= - \boldsymbol{\mathbb{E}}(\log_2{p(X | Y)}) =  \boldsymbol{\mathbb{E}}(h(X | Y))$$
    
    On doit donc calculer le terme $h(X | Y)=-\log_2{(p(X | Y))}.$ Ceci est aisément obtenu en considérant la vraisemblance du canal de la
    manière suivante
    
    $$p(X | Y) =  \frac{p(Y|X)}{\sum_{x \in \mathcal{X}}{p(Y|X=x)}}.$$

    Le calcul de $\boldsymbol{\mathbf{H}}(X|Y)$ peut alors se faire par Monte-Carlo en utilisant un estimateur asymptotiquement sans biais
    de cette quantité. En effet, par ergodicité, on a
    
    $$\boldsymbol{\mathbf{H}}(X|Y)= \boldsymbol{\mathbb{E}}({h(X | Y)}) = \lim_{N \rightarrow +\infty}\frac{1}{N} \sum_{n}{h(x(n)| y(n))}$$
    
    où $h(x(n)| y(n))=\log_2(p(x(n) | y(n)))).$

    La procédure globale pour l'estimation par monte-Carlo peut alors se résumer comme suit

    1.  Tirer aléatoirement et uniformément des symboles issus de la constellation d'intérêt,

    2.  Calculer pour chaque couple $(x(n),y(n))$ $h(x(n) | y(n))$ et moyenner.

