## Information mutuelle

Pour caractériser la similarité au sens statistique de deux variables aléatoires, on peut utiliser ce que l'on appelle l'information mutuelle qui est définie comme suit

```{prf:definition} Information mutuelle

Soit $X, Y$ deux v.a. discrètes, l'information mutuelle entre $X$ et $Y$ est définie par 

$$\begin{aligned}
\boldsymbol{\mathbf{I}}(X;Y) & = - \sum_{x \in \mathcal{X}} \sum_{y \in \mathcal{Y}} {p(X=x,Y=y) \log_2{(\frac{p(X=x)p(Y=y)}{p(X=x,Y=y)})}}\nonumber\\
&= - \boldsymbol{\mathbb{E}}(\log_2{(\frac{p(X)p(Y)}{p(X,Y)})}) \geq 0
\end{aligned}$$
```

L'extension au cas vectorielle est immédiate. 


```{prf:property}
1. **Positivité :** 

 $$\mathrm{I}(X ; Y) \geq 0$$

2.  **Borne sup. :**
    
    $$\mathrm{I}(X ; Y) \leq \min (\mathrm{H}(X), \mathrm{H}(Y))$$

3.  **Symétrie :** 

    $$\mathbf{I}(X ; Y)=\mathbf{I}(Y ; X)$$

4.  **Information propre :**  

    $$I(X ; X)=\mathbf{H}(X)$$

5.  **Liens avec entropie, entropie conjointe et conditionnelle :**

    $$\begin{aligned}
    \boldsymbol{\mathbf{I}}(X;Y) & =  \boldsymbol{\mathbf{H}}(X) -\boldsymbol{\mathbf{H}}(X|Y) \nonumber\\
    &=\boldsymbol{\mathbf{H}}(Y)-\boldsymbol{\mathbf{H}}(Y|X) \nonumber \\
    &=\boldsymbol{\mathbf{H}}(X)+\boldsymbol{\mathbf{H}}(Y)-\boldsymbol{\mathbf{H}}(X,Y)
    \end{aligned}$$

6.  **Conditionnement :**
    
    $$\mathrm{I}(X ; Y \mid Z) \triangleq \mathrm{H}(X \mid Z)-\mathrm{H}(X \mid Y, Z) \geq 0$$

7.  **Chain rule :**
    
    $$\mathbf{I}\left(X_{1}, X_{2}, \cdots, X_{n} ; Y\right)=\sum_{i=1}^{n} \mathbf{I}\left(X_{i} ; Y \mid X_{i-1}, \cdots X_{1}\right)$$
```
Le lien avec les autres quantité de théorie de l\"information est donné
par le diagramme dit de Venn suivant

::: center
![image](relationsentropies){height="6cm"}
:::

Dans le cas de variables aléatoires, on peut alors donner la définition suivante

$$I(X ; Y)=-\int f(x, y) \log _{2}\left(\frac{f(x) f(y)}{f(x, y)}\right) d x d y \geq 0$$

