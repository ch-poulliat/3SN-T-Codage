## Décodage par Maximum de Vraisemblance

Dans cette section, on s'intéresse au décodage par maximum de vraisemblance (ou encore appelé *MLSE*) comme défini auparavant. Onexplicite ici comment ce type de décodage s'instantie dans le cas des codes convolutifs.

### Critère de décodage MLSE

Pour rappel, le critère MLSE se décline toujours sous la forme

$$\begin{aligned}
\hat{{\bf c}}&= \mathrm{arg} \max_{{\bf c}}{p({\bf y} | {\bf  c})} \nonumber \\
&=&  \mathrm{arg} \max_{{\bf c}}{\prod_n{p(y_n | {c_n})}} \nonumber \\
\end{aligned}$$

La dernière égalité venant du fait que l'on considère une canal sans mémoire à entrées antipodales (BPSK) pour première présentation. Si on considère un code convolutif avec fermeture de treillis avec un treillis comportant $L$ sections, et en reprenant les notations précédentes sur les codes convolutits, on peur alors écrire 


$$\begin{aligned}
\hat{{\bf c}}&= \mathrm{arg} \max_{{\bf c}}{\prod_{k=1}^L{p({ \bf y_k} | {\bf c_k})}} \nonumber 
\end{aligned}$$

où ${ \bf y_k}=(y_k^{(1)}, \cdots, y_k^{(n_c)})$ et ${ \bf c_k}=(c_k^{(1)}, \cdots, c_k^{(n_c)})$.

On aura donc finalement

$$p({ \bf y_k} | {\bf c_k})=\prod_{n=1}^{n_c}{p(y_k^{(n)}|c_k^{(n)})}.$$

En posant $\lambda_k({\bf c_k})=-log{(p({ \bf y_k} | {\bf c_k}))}$, toujours positif, il vient 

$$\begin{aligned}
\hat{{\bf c}}&= \mathrm{arg} \min_{{\bf c}}{\sum_{k=1}^L{\lambda_k({\bf c_k})}} 
\end{aligned}$$

### Algorithme de Viterbi

L'estimation de la séquence la plus vraisemblable sera réalisée efficacement à l'aide de l'algorithme de Viterbi, premier à proposer cette solution. L'idée originale de Viterbi est d'utiliser le treillis associé au code convolutif pour énumérer efficacement l'ensemble des chemins possibles. En utilisant, le treillis, cet algorithme permet à
chaque section de treillis de ne garder que les $|\mathcal{S}|$ chemins les plus vraisemblables terminant dans chaque état. Rappelons que, de par la représentation d'état, on a ${\bf c_k(s_{k-1},s_k)}$, ie. les labels des bits codés émis ${\bf c_k}$ qui sont une fonction déterministe de l'état de départ $s_{k-1}$ et l'état d'arrivée $s_k$. On
a alors les propriétés suivantes :

```{prf:property} 

1.  Correspondance entre espace des séquences et des états


2.  Chaque chemin sur le treillis représente une séquence de bits codés
    émis possibles :
```

En effet, en utilisant le fait que

$$\left \{ c[n] | n=1 \cdots N \right\} \Longleftrightarrow \left \{ {\bf c_k} | k=1 \cdots L \right\}$$

un simple jeu de réécriture permet d'avoir

$$\begin{aligned}
\hat{{\bf c}}&= \mathrm{arg} \min_{{\bf c}}{\sum_{k=1}^L{\lambda_k({\bf c_k})}}  \nonumber \\
&   \hspace{2cm} {\huge \Updownarrow}\\
\hat{{\bf c}}&= \mathrm{arg} \min_{s_k}{\sum_{k=1}^L{\lambda_k({\bf c_k}(s_{k-1},s_k))}} \nonumber\\
&=\mathrm{arg} \min_{s_k}{\sum_{k=1}^L{\lambda_k(s_{k-1},s_k)}} 
\end{aligned}$$

Pour la section de treillis $n$, à l'état $s_n=s$, on peut alors écrire
 
$$\begin{aligned}
\Lambda_n(s_n) &=  \underset{\lbrace s_0, s_1, \cdots, s_{n-1}, s_n \rbrace}{\operatorname{min}}{\sum_{k=0}^{n}{\lambda_k(s_{k-1},s_k)}} \nonumber \\
& =\underset{\lbrace s_{n-1} \rightarrow s_n \rbrace}{\operatorname{min}} \left\{  \left\{ \underset{\lbrace s_0, \cdots, s_{n-1}\rbrace}{\operatorname{min}} {\sum_{k=0}^{n-1}{\lambda_k(s_{k-1},s_k)}} \right\} + \lambda_n(s_{n-1},s_n) \right\} \nonumber \\
& =\underset{\underbrace{\left\{s_{n-1} \rightarrow s_n \right\}}_{\mbox{transitions possibles}}}{\operatorname{min}} \left\{ \Lambda_{n-1}{(s_{n-1})} + \lambda_n(s_{n-1},s_n) \right\}
\end{aligned}$$

La procédure complète est alors donnée par 

```{prf:algorithm} Algorithme de Viterbi

-   Pour chaque section $n$ ($n=1 \cdots N$), pour chaque état $s_n=s$ ($s=0 \cdots |\mathcal{S}|$) :

    1.  calculer $\Lambda_n$ tel que
    
        $$\Lambda_n{(s_{n})}=\underset{\left\{s_{n-1} \rightarrow s_n \right\}}{\operatorname{min}} \left\{ \Lambda_{n-1}{(s_{n-1})} + \lambda_n(s_{n-1},s_n) \right \}$$

    2.  stocker l'état précédent $s_{n-1}$ : pour chaque état $s_n$, on peut donc associer une séquence *survivante* $\left\{s_0, \cdots, s_n \right\}$ de métrique cumulée associée $\Lambda_n{(s_{n})}$)

-   A la fin du treillis, il ne reste plus que $|\mathcal{S}|$ chemins possibles, alors par parcours arrière (*traceback*) des états du treillis

    $$\hat{{\bf s}}= \left\{s_0, s_1, \cdots, s_{L-1}, s_L | \underset{s_L}{\operatorname{argmin}}\left\{\Lambda_{L}(s_L) \right\} \right\}$$

    ce qui équivaut compte tenu que
    
    $$\hat{{\bf s}}=\left\{s_0, s_1, \cdots, s_{L-1}, s_K \right\} \leftrightarrow \hat{{\bf u}}=\left\{u_1, s_2, \cdots, u_{K-1}, u_K \right\}$$
    
    à sélectionner la séquence d'information la plus probable (Hard Output, HO) en utilisant $(s_{n-1},s_n) \rightarrow u_n$.
```

Si le treillis est fermé lors de l'étape de codage (retour à zéro), le dernier état est donné systématiquement par $\Lambda_{L}(s_0)$.

#### Cas du décodage à entrées dures (Hard Inputs (HI)) 

Le modèle de canal est alors donné par

$$y_n=c_n \oplus e_n, \forall n=1,\cdots, N.$$ 

Dans le cadre d'un décodage dure, on a alors

$$\begin{aligned}
\lambda_k(s_{k-1},s_k)&=d_H({\bf y_k},{\bf c_k}) \nonumber \\
&=\sum_{m=1}^{n_c}{d_H(y_k^{(m)},c_k^{(m)})} \nonumber \\
&=\sum_{m=1}^{n_c}{y_k^{(m)} \oplus c_k^{(m)}}
\end{aligned}$$

Le mot de code sélectionné sera donc bien le mot de distance de Hamming cumulée la plus faible.

#### Cas du décodage à entrées "souples" 

Le modèle de canal est alors donné par

$$y_n=c_n + b_n, \;\;  \forall n=1,\cdots, N.$$

où $b_n \sim \mathcal{N}(0,\sigma^2_b).$

et donc

$$\begin{aligned}
p(y_n|c_n) & \propto  e^{-\frac{(y_n-c_n)^2}{2 \sigma_b^2}} \nonumber
\end{aligned}$$

Dans le cadre d'un décodage souple, après calcul direct, on a alors

$$\begin{aligned}
\lambda_k(s_{k-1},s_k)&= d_E({\bf y_k},{\bf c_k}) \nonumber \\
&=\sum_{m=1}^{n_c}{|y_k^{(m)}-c_k^{(m)}|^2}
\end{aligned}$$

Le mot de code sélectionné sera donc bien le mot de distance euclidienne cumulée la plus faible.

On peut encore simplifié le problème en développant les termes $|.|^2$, en supprimant les termes constants et/ou communs à chaque métrique de
branche de la section courante du trellis, on obtient une nouvelle métrique:

$$\begin{aligned}
\tilde{\lambda}_k(s_{k-1},s_k)&=-\sum_{m=1}^{n_c}{y_k^{(m)}c_k^{(m)}}
\end{aligned}$$

On définit alors finalement par 

$$\begin{aligned}
\Gamma_k(s_{k-1},s_k)&=\sum_{m=1}^{n_c}{y_k^{(m)}c_k^{(m)}}
\end{aligned}$$ 

la métrique de branche comme étant la corrélation déterministe partielle entre la séquence observée et le mot de codes émis. Comme on a changé le signe de cette métrique, il convient alors de remplacer l'opération de $\min$ par $\max$ dans l'algorithme de Viterbi présenté. On interprète alors cela comme une maximisation de l'intercorrélation entre le mot émis et la séquence observée.

#### Cas du décodage à entrées "souples" (Soft Inputs (SI)), modulation $M$-aire sur canal Gaussien.

On s'intéresse maintenant au cas où le mot émis est mappé sur une constellation d'ordre élevée. Pour commencer, on considère que l'on a un ordre de constellation $M=2^{n_c}$, ie. chaque label ${\bf c_k}$ est **directement** mappé sur un symbole de la constellation. On note $x_k=\mathcal{M}({\bf c_k})$ où $\mathcal{M}(.)$ est l'opérateur de mapping.

Le modèle de canal est alors donné par

$$y_n= x_n + b_n, \;\;  \forall n=1,\cdots, L$$

où $b_n$ est un bruit blanc Gaussien complexe circulaire suivant une loi $\mathcal{CN}(0, \sigma_b^2)$, ie. $b_n= b_{I,n}+i b_{Q,n}$ où $b_{I,n}$ et $b_{Q,n}$ suivent une loi normale réelle $\mathcal{N}(0,\sigma_b^2/2)$. On a donc 

$$\begin{aligned}
p(y_n|x_n) & =  p(b_n) \nonumber\\
& =  p(b_{I,n},b_{Q,n}) \nonumber\\
&\propto  e^{-\frac{|y_n-x_n|^2}{\sigma_b^2}}
\end{aligned}$$

Le décodage ML s'écrit comme précédemment 

$$\begin{aligned}
\hat{{\bf c}}&=\mathrm{arg} \max_{{\bf c}}{p({\bf y} | {\bf  c})} \nonumber \\
&=  \mathrm{arg} \max_{{\bf c}}{\prod_n{p(y_n | {c_n})}} \\
&=  \mathrm{arg} \max_{{\bf x}}{\prod_n{p(y_n | {x_n})}}
\end{aligned}$$

Comparé au cas binaire précédent, on a directement accès à $p(y_n | {x_n}), \forall n$. Dans ce cas la métrique de branche se simplifie comme suit 

$$\begin{aligned}
\lambda_k(s_{k-1},s_k)&=d_E(y_k, x_k) \nonumber \\
&=|y_k-x_k|^2
\end{aligned}$$

On retrouve là encore le fait que la séquence retenue au final sera la séquence la plus proche de la séquence reçue. On peut également simplifier le décodage en considérant la métrique 

$$\begin{aligned}
\tilde{\lambda}_k(s_{k-1},s_k)&=&-2\text{Re}{\lbrace y_k x^*_k\rbrace} + |x_k|^2
\end{aligned}$$ 

Ceci s'interprète comme une corrélation "corrigée" par la puissance du symbole considéré.

Si la modulation est à module constant, on pourra simplifier en

$$\begin{aligned}
\Gamma_k(s_{k-1},s_k) & =  2\text{Re}{\lbrace y_k x^*_k \rbrace}
\end{aligned}$$

Dans ce cas, on revient à une maximisation de corrélation entre séquence de symboles reçus et séquence de symboles émis.

#### Cas du décodage à entrées "souples" (Soft Inputs (SI)), modulation $M$-aire à bits entrelacés sur canal Gaussien 


Pour simplifier la complexité induite par l'utilisation d'un code adapté à l'ordre de modulation (modulation codées en treillis dont le cas
précédent est un cas trivial), on considère un schéma pour lequel on place un entrelaceur entre le code et la modulation. Le mot de code
${\bf c}=[c_1, \cdots, c_N]$ est entrelacé par l'entrelaceur $\Pi$. On obtient alors une séquence de symboles ${\bf x=[x_1, \cdots,x_{N_s}]}$
obtenus en regroupant les bits codés entrelacés en groupes de $m$ bits tels que ${\bf x_n}=[x_n^1,\cdots, x_n^m]$. $[x_n^1,\cdots, x_n^m]$
définit l'étiquette binaire pour le mapping sur le symbole ${\bf s_n}=\mathcal{M}({\bf x_n}) \in \mathbb{C}$. L'entrelaceur $\Pi$
définit une relation bijective 

$$\begin{aligned}
\pi : \left[1, \cdots, N\right]& \mapsto & \left[1, \cdots N_s \right] \times  \left[1, \cdots m \right] \nonumber \\
k & &(k',i)
\end{aligned}$$ 

entre le bit codé $c_k \in \lbrace 0,1 \rbrace$ et le $i$-ème bit $x_{k'}^i$ du symbole $M$-aire ${\bf x_{k'}}$. On a $N_s=N/m$.

$$\mathcal{M}: x \rightarrow s$$ 

définit la fonction bijective de mapping. Au niveau du récepteur, un décodage conjoint code-modulation n'est plus possible. On réalise alors une démodulation souple qui va
estimer de manière souple les bits du mots de codes. Cette information souple est donnée sous la forme d'une log-vraisemblance ou d'un log-rapport de vraisemblance (LLR). La quantité obtenue traduit le fait que l'on a transformé un canal vectoriel $M$-aire en $m$ canaux binaires équivalents dont les caractéristiques moyennes dépendent de la
modulation et du mapping utilisés. La définition suivante donne les quantités ***souples*** que l'on peut estimer sur les bits codés émis.


On suppose la transmission de symboles $M$-aire sur canal Gaussien avec $M=2^m$. Les vecteurs binaires $x[n]=[x^1[n], \cdots, x^m[n]] \in \mathcal{X}=\{0,1\}^m$ sont "mappés"
sur des symboles $s[n] \in \mathcal{S} \subset \mathbb{C}$. On suppose que les symboles $x[n]$ (et donc $s[n]$) sont équi-distribués. Les symboles observés sont donnés par ${\bf y=[y_1, \cdots, y_{N_s}]}$. On supposera le canal sans mémoire. On peut définir alors deux quantités relatives à une décision *souple* : 

1.  ***log-vraisemblance/métrique bit ML :***

    $$\lambda^i(y_{k'},b)=\log{\sum_{{\bf x} \in \mathcal{X}_b^i}} { p({\bf y_{k'}}| {\bf x})}, \; \forall i=1, \cdots, m.$$
    
    $\mathcal{X}_b^i$ est le sous-ensemble des symboles ${\bf x} \in \mathcal{X}$ ayant $x_i[n]=b \in \lbrace 0,1 \rbrace$ dans leur étiquette binaire associée.

2.  ***LLR associé au bit $x_i[n]$***:

L'expression $\lambda^i(y_{k'},b)$ est en fait dérivée de la vraisemblance de l'obersvation ${\bf y_{k'}}$ sachant le bit de label $x_{k'}^i$. Ainsi on a

$$\begin{aligned}
p({\bf y_{k'}}|x^i=b)&=\sum_{{\bf x} \in \mathcal{X}} { p({\bf y_{k'}}| {\bf x})p({\bf x}|x^i=b)} \nonumber \\
%
&= \frac{1}{2^{m-1}}\sum_{{\bf x} \in \mathcal{X}_b^i} { p({\bf y_{k'}}| {\bf x})}
\end{aligned}$$ en notant que
$$p({\bf x})|x^i=b)=\left\lbrace\begin{array}{ll}
2^{-(m-1)} &, \; \mathrm{si} \; x^i= b \\
0 &,\; \mathrm{sinon}
\end{array} \right.$$ 

En passant au $\log$ et en ne gardant pas le terme constant, on obtient la métrique voulue.

Le décodage ML du mot de code émis est alors réalisé à partir des métriques bit supposées indépendfantes après entrelacement supposé
parfait. La règle de décision est alors donnée par

$$\begin{aligned}
\hat{{\bf c}}&= \mathrm{arg} \max_{{\bf c}}{\sum_{n=1}^N{\lambda^i({\bf y_{k'}},c_n)}}
 \end{aligned}$$

Pour un code convolutif, si on considère un décodage par Viterbi sur le treillis cela revient à considérer le probleme suivant 

$$\begin{aligned}
\hat{{\bf c}}&= \mathrm{arg} \max_{{\bf c}}{\sum_{k=1}^L {\lambda_k(s_{k-1},s_k)}}
\end{aligned}$$

où, avec quelques abus de notation, la métrique de branche s'exprime comme

$$\lambda_k(s_{k_1},s_k)=\sum_{l=1}^{n_c}{\lambda^i(y_{k'},c_k^{l})}$$

où ${\lambda^i(y_{k'},c_k^{l})}$ représente la log-vraisemblance associée au bit codé $c_k^{l}$ quand on redéfinit l'entrelacement comme étant la fonction 

$$\begin{aligned}
\pi:  \left[1, \cdots , L \right] \times \left[ 1, \cdots , n_c \right]  & \mapsto & \left[ 1, \cdots, N_s \right] \times \left[ 1,\cdots, m \right] \nonumber \\
(k,l) &  & (k',i) \nonumber
\end{aligned}$$ 


où $N_s$ est le nombre de symboles modulés codés émis sur le canal ($N_s=(L . n_c)/m$)