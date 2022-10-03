## Démodulation MAP bit et systèmes BICM.


Nous étendons ici les notions de détection souple mise en exergue dans le cas binaire aux cas de sysèmes opérant avec modulations d'ordre élevé.

### Démodulation souple : détection MAP bit.

L'avènement des systèmes de codage à décodage souple et itératifs s'est accompagné du développement de la détection "souple" des modulations.
Comme nous le verrons par la suite, l'utilisation de codes dîts "modernes" tels que les turbo-codes (déjà vieux de 30 ans) et les codes LDPC (presque 60 ans...) n'est utilisée à son plein potentiel que si à l'entrée du décodeur, on fournit une entrée "souple", souvent homogène à un LLR. Nous allons donc voir le principe de la démodulation souple, ie. la
détection MAP d'un bit appartenant à un symbole non binaire $M$-aire qui est associé à une constellation $M$-aire.

Soit le vecteur $m$-binaire de bits $\textbf{x}[n]=[x_1[n] \cdots x_m[n]]$ qui représente l'étiquette binaire qui sera utilisée pour pour identifier un symbole d'une constellation$M$-aire, $m=\log_2{(M)}.$ Les symboles sont supposés indépendants et équi-distribués. Chaque vecteur $\textbf{x}[n]$ est alors "mappé" sur un symbole dune constellation $M$-aire $\mathcal{S}$ de cardinalité $|\mathcal{S}|=M$ en suitvant la règle de mapping donnée par la fonction bijective suivante

$$\begin{aligned}
\mathcal{M} : \mathbb{F}_2^m & \longrightarrow & \mathcal{S} \subset \mathbb{C} \nonumber \\
x & \mapsto & s=\mathcal{M}(x)
\end{aligned}$$

Un critère classique de détection symbole est donné par la règle du maximum de vraisemblance donné par

$$\hat{s}_n = \mathrm{arg} \max_{s_n}{p(y[n] | s[n]) },$$ 

où $p(y[n]|s[n])$ est la vraisemblance associée à l'observation $y[n].$ Cette dernière est supposée connue au récepteur car on sait caractériser la loi de transition du canal. De manière similaire au cas bloc, on peut également appliqué un critère MAP symbole qui est donné par 

$$\hat{s}_n = \mathrm{arg} \max_{s_n}{p(y[n] | s[n]) } p(s[n]),$$ 

si on possède un a priori sur le symbole $s[n].$ Maximum de vraisemblance et MAP sont équivalents si on a un apriori uniforme (ce qui est équivalent à ne pas en avoir...), dans ce cas $p(s[n])=1/M.$ Ces deux dernières règles sont utiles pour un décodage à sorties "dures". Après "demapping", ie. appliquaton de la règle de mapping inverse donnée par
$\mathcal{M}^{-1}(.),$ on pourra fournir des bits décidés à un décodeur de canal utilisant des entrées dures/décidées. Cependant, si on considère que le code de canal utilisé pour la transmission est un code binaire et que son décodage peut faire usage d'entrées \"souples\", ie. sous forme de probabilités bit ou de manière équivalente sous forme de
LLRs, il convient alors de dériver une règle de démodulation à décisions "souples" au niveau bit. On va donc dériver un critère de détection MAP bit dont l'expression dans le domaine lograrithmique est donnée par

```{prf:definition} Démodulation MAP bit

Soit $\textbf{x}[n]=[x_1[n] \cdots x_m[n]]$ le vecteur binaire de $m$ bits correspondant à l'étiquetage du symbole $s[n]$ d'une constellation
$M$-aire $\mathcal{S},$ le log-rapport de probabilité est alors donné par 

$$\begin{aligned}
L(x_i[n])&=  \log{\left( \frac{p(x_i[n]=0\mid y[n])}{p(x_i[n]=1\mid y[n])}\right)}\nonumber \\
&=  \log{\left( \frac{\sum_{s[n] \in \mathcal{S}_0^i}{p(y[n]|s[n])p(s[n])}}{\sum_{s[n] \in \mathcal{S}_1^i}{p(y[n]|s[n])p(s[n])}} \right)}
\end{aligned}$$ 

où $\mathcal{S}_0^i\subset \mathcal{S}$ (resp. $\mathcal{S}_1^i$) est le sous ensemble des symboles $s \in \mathcal{S}$ tels que le $i$-ième bit $x_i[n]$ du vecteur $x[n],$ tel que $s[n]=\mathcal{}$ est le bit $'0'$ (resp. le $i$-ième bit $x_i[n]$ du vecteur $x[n]$ est le bit $'1'$). $p(s[n])$ est la probabilité a priori de $s[n]$ qui sera considéré comme uniforme pour la plupart des cas d'intérêt.
```

Comme une a une relation bijective entre $s[n]$ et $x[n],$ on peut donner également donner l'expression

$$\begin{aligned}
L(x_i[n])&= \log{\left( \frac{p(x_i[n]=0\mid y[n])}{p(x_i[n]=1\mid y[n])} \right)}\nonumber \\
&=  \log{\left( \frac{\sum_{x[n] \in \mathcal{X}_0^i}{p(y[n]|x[n])p(x[n])}}{\sum_{x[n] \in \mathcal{X}_1^i}{p(y[n]|x[n])p(x[n])}} \right)}
\end{aligned}$$

où $\mathcal{X}_0^i \subset \mathbb{F}_2^m$ est l'ensemble des vecteurs de $\mathbb{F}_2^m$ de composante $i$ nulle (définition similaire pour $\mathcal{X}_1^i$). On aura également $p(y[n]|x[n])=p(y[n]|s[n]=\mathcal{M}(x([n]).$ Quand une a priori sera disponible, ce sera souvent un apriori indépendant pour chaque bit du vecteur $x[n],$ ce qui s'écrit comme 

$$p(x[n])=\prod_{i=1}^m{p(x_i[n])}.$$ 

Cette dernière relation pourra également s'écrire à partir des LLRs a priori associés.

### Capacité des systèmes BICM

Les capacités à entrées contraintes dérivées au chapitre précédent sont déterminées pour des systèmes qui opérent (codent) dans l'espace de la modulation. Pour des raisons
pratiques (facilité de design, complexité), la plupart des schémas codés considèrent une concaténation série entre code binaire et une modulation $M=2^m$-aire éventuellement séparé par un entrelaceur, souvent dénommés par l'acronyme BICM pour ***Bit interleaved coded modulation***. Dans la plupart des système BICM, le décodeur de canal utilise des entrées "souples", il faut donc utiliser un système dît à ***démodulation souple***. L'ajout d'un entrelaceur dépend du système de codage utilisé. Généralement si le code
externe est un code défini par un treillis ou un code en bloc court, il faut ajouter un entrelaceur. Si on a un code de type LDPC, nous verrons que ce n'est pas utile. Une fois le système spécifié, on peut maintenant se poser la question des performances asymptotiques des systèmes BICM, ie. qu'on se pose la question de la sous-optimalité éventuelle de ces systèmes. Comme on démodule pour se ramener à l'estimation d'une information binaire, si on inclut symboliquement l'opération de modulation/démodulation dans le canal, alors un système BICM peut être vu comme un canal constitué de $\log_2(M)$ canaux parallèles *indépendants*, l'indépendance étant garantie théoriquement par l'ajout de l'entrelaceur entre le code et la modulation. La capacité atteignable dépend du mapping utilisé et est donnée par

$$C_{\mathrm{bicm}}=m-\frac{1}{2}\sum_{k=0}^{m-1}\sum_{c=0}^{1}{\mathbb{E}\left( \log_2{\left(\frac{\sum_{s_i \in \mathcal{S}}{p(y|s_i)}}{\sum_{s_j \in \mathcal{S}_c^k}{p(y|s_j)}} \right)}\right)}$$

On peut montrer la formule suivante, plus commode à utiliser et interpréter :

$$C_{\mathrm{bicm}}=\sum_{k=1}^m \boldsymbol{\mathbf{I}}(X_k;Y) \leq C_{AWGN},$$

où

$$\boldsymbol{\mathbf{I}}(X_k;Y)=1-\mathbb{E}_{X_k,Y}{(\log_2(1+e^{-(1-2 X_k)L(X_k)}))}.$$

$\boldsymbol{\mathbf{I}}(X_k;Y)$ est la capacité binaire associée au canal associé au $k$-ième bit du symbole après marginalisation bit. Notons également que $L(X_k)$ est une fonction implicite de $Y.$ A partir de ces expressions, on peut alors facilement calculer une estimée

$$\hat{I}({X_k},{Y})=1-\frac{1}{N_k} \sum_n{(\log_2(1+e^{-(1-2 x_k[n])L(x_k[n])}))}.$$

En général pour les modulations linéaires, le mapping de Gray permet d'être quasi-optimal pour les efficacités moyennes à grandes.
