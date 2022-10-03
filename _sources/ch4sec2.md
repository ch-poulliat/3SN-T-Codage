## Turbo-codes série

```{figure} tcserie.png
---
name: turbo-serie-fig
---
Structure d'un turbo-code série avec deux codeurs.
```

La figure {numref}`turbo-serie-fig` représente une autre concaténation possible à savoir la concaténtaion série. Le processus à l'émetteur est le suivant

-   $K$ bits d'information sont codés avec le codeur $1$ (code externe),

-   les bits codés sont entrelacés et puis codés par le codeur $2$ (code interne).

Dans ce cadre, on a un rendement global (hors poinçonnage) correspondant au produit des rendements des deux codes internes 

$$R=R_i R_o$$ 

où $R_i$ (resp. $R_o)$ est le rendement du code interne (resp. externe).


L'architecture du décodeur est alors donnée par la figure {numref}`turbo-decoder-serie-fig`:

```{figure} decserie.png
---
name: turbo-decoder-serie-fig
---
Structure du décodeur itératif pour la concaténation série
```


Les principales différences par rapport au cas de la concaténation parallèle sont les suivantes:

-   les deux décodeurs associés différents du cas parallèle,

-   le premier codeur peut le pas ètre récursif.



Pour le décodage, le décodeur souple associé au code interne est le même
que celui d'un turbo-code parallèle, ie. que l'on donne une information
souple sur les bits d'"information" du codeur interne. Pour le code
interne, le décodeur doit fournir une information extrinsèque sur
l'ensemble des bits codés et non plus seulement sur les bits
d'information. Le critère MAP associé est alors modifié de la manière
suivante

$$\begin{aligned}
L_1(c_n^{(m)}) &= &{\max_{\mathcal{C}^{+}}}^*{\left(\tilde{\alpha}_{n-1}(s')+\tilde{\gamma}_n(s',s)+\tilde{\beta}_{n}(s)\right)} \nonumber \\
& &-{\max_{\mathcal{C}^{-}}}^*{\left(\tilde{\alpha}_{n-1}(s')+\tilde{\gamma}_n(s',s)+\tilde{\beta}_{n}(s)\right)} \\
& =& L_2^e(c_n^{(m)})+L_1^e(c_n^{(m)}) \\
\tilde{\gamma}_n(s',s)&=&\sum_{m=1}^{n_c}{c_n^{(m)}(s',s) \frac{L_2^e(c_n^{(m)}(s',s))}{2}}
\end{aligned}$$ 

où l'on a les notations suivantes:

$$\mathcal{C}^{+} = \{ (s',s) \; \mathrm{ o\grave{u} } \; (s_{n-1}=s') \mapsto (s_{n}=s)| c_n^{(m)}=+1 \}$$

$$\mathcal{C}^{-} = \{ (s',s) \; \mathrm{ o\grave{u} } \; (s_{n-1}=s') \mapsto (s_{n}=s)| c_n^{(m)}=-1 \}$$