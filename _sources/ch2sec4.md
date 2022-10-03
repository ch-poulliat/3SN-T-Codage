## Décodage MAP bit/symbole pour un code en bloc

On va maintenant s'intéresser à un critère MAP symbole, le symbole étant ici un bit. Ce critère diffère du MAP séquence ou ML. L'idée ici est de
calculer la probabilité a posteriori d'un bit d'information (ou codé comme on le verra après) sachant l'ensemble de observations. Ceci est
donné par la définition suivante si on considère une séquence codée $c_n \in \{ 0,1 \}$ de taille $N$ 

```{prf:definition} Décodage MAP bit 

$$\begin{aligned}
\hat{c}_n &=& \mathrm{arg} \max_{c_n}{p(c_n | {\bf y}) } \nonumber \\
&=& \frac{1-\mathrm{signe}(L(c_n))}{2}
\end{aligned}$$ 

avec

$$L(c_n)=\log{\left[\frac{p(c_n = 0 | {\bf y})}{p(c_n = 1 | {\bf y})}\right]}$$
```

La quantité $L(c_n)$ est ce que l'on appelle le LLR (*Log-LikelihoodRatio*) a posteriori associé au bit $c_n$.

Le critère est une conséquence du fait que l'on considère une variable binaire. En effet, si on considère le bit $c_n$, alors le test de
décision statistique binaire associé donne 

$$\hat{c}_n = \mathrm{arg} \max_{c_n}{p(c_n | {\bf y}) }=0$$ 

si


$$p(c_n=0 | {\bf y}) > p(c_n=1 | {\bf y}).$$

Par passage au $\log$ et définition du LLR associé à $u_n$ on obtient alors $L(c_n)>0$. De la même manière, on aura $\hat{c}_n =1$ si
$L(c_n)<0$. On a donc la relation $\mathrm{signe}(L(c_n))=1-2 u_n$ qui nous définit un mapping bijectif entre le signe du LLR et la valeur
binaire. Ce mapping bijectif correspond d'ailleurs à un mapping de type BPSK : $\{`0' \leftrightarrow +1, `1' \leftrightarrow -1 \}$. Compte
tenu de cette relation directe, il est souvent plus commode de directement considérer la version "mappée/modulé" du bit (cas des observations souples
canaux souples), de sorte que l'on considérera de manière indifférenciée $c_n=0/1$ et $c_n=\pm 1$ dès lors le contexte en suffisamment clair.
Ainsi, on pourra adopter la règle MAP suivante

$$\begin{aligned}
\hat{c}_n &=& \mathrm{arg} \max_{c_n}{p(c_n | {\bf y}) } \nonumber \\
&=& \mathrm{signe}(L(c_n))
\end{aligned}$$

Le LLR associé à $c_n$ peut être associé à une mesure de fiabilité de la décision. En effet, $\mathrm{signe}(L(u_n))$ est identifiable à une décision \"dure\" du bit à laquelle on peut associer une mesure de fiabilité de cette décision grâce à $|L(u_n)|$. Un algorithme qui fournit en sortie des informations homogènes à des LLRs (ou symboles bruités) est appelé ***algorithme à sorties souples (Soft Outputs, SO)*** par opposition à des algorithmes qui fournissent une version décidée des symboles dénommés ***algorithme à sorties dures (Hard Outputs, HO)***. Par analogie, si les entrées sont des symboles décidés, on parle d'algorithme à entrées dures (Hard Input, HI) par opposition à des algorithmes à entrées souples (Soft Inputs, SI) prenant en compte des symboles bruités ou des entrées représentant des statistiques suffisantes. Comme pour le cas du décodage ML, la mise en oeuvre d'un algorithme de décodage efficace dépend de la structure du code sous-jacent. Nous explorerons différents types de détecteur symbole MAP : les algorithme de type BCJR qui acte sur des treillis et et qui seront appliqués à des codes convolutifs ou codes en blocs. Les algorithmes itératifs de type Belief Propagation qui s'appliquent sur des structure graphiques des codes, comme pour les codes Low Ddensity Parity Check.