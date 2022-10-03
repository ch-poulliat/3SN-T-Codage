::: frame
:::

::: frame
### Plan
:::

# Codes LDPC

## Définitions et notations {#définitions-et-notations .unnumbered}

::: frame
### Codes LDPC

#### Introduction

-    : Gallager, codes LDPC régulier, décodeur $A$ et $B$\

-    : Tanner, codes définis sur les graphes.\

-    : MacKay, décodage par BP\

-    : Richardson et Urbanke, codes LDPC irréguliers et évolutions de
    densités.
:::

::: frame
### Efficacité de certains systèmes de codage

::: center
![image](Image2.png){width="90%"}
:::
:::

::: frame
### Codes en bloc linéaires

#### Quelques définitions

On considère des codes définis sur le corps binaire
$\mathbb{F}_2=GF(2)$.

::: block
Codes linéaires en blocs

-   Un code en blocs binaire $\mathcal{C}(N,K)$ de longueur $N$ est une
    application $g(.)$ de l'ensemble $\mathbb{F}_2^K =\{0, 1 \}^K$ vers
    l'ensemble $\mathbb{F}_2^N =\{0, 1\}^N$ qui associe à tout bloc de
    données $\bf{u}$ un mot de code $\bf{c}$. $$\begin{aligned}
    g : \mathbb{F}_2^K & \rightarrow & \mathbb{F}_2^N \nonumber \\
    {\bf u} & \mapsto & {\bf c} = g({\bf u})
    \end{aligned}$$

-   $\#$ mots de code : $2^K$.

-   Rendement: $R = K/N$ ($K$ symb. d'inf., $N$ symb. codés).

-   $\mathcal{C}(N,K)$ est dit linéaire si $g(.)$ est une application
    linéaire (les mots de codes sont un sous-espace vectoriel de
    $\mathbb{F}_2^N$).
:::
:::

::: frame
### Codes en bloc linéaires

#### Matrice génératrice

::: block
Matrice génératrice

-   On note ${\bf c}=[c_0, \ldots, c_{N-1}]$ et
    ${\bf u}=[u_0, \ldots, u_{K-1}]$

-   la matrice génératrice $\mathbf{G}$ de dimensions $K \times N$ est
    définie comme étant l'application linaire définie comme
    $${\bf c}= {\bf u} \mathbf{G}$$

-   Espace du code :
    $\mathrm{Im}(\mathcal{C})=\{ {\bf c} \in \mathbb{F}_2^N | {\bf c}= {\bf u} \mathbf{G}, \;\; \forall {\bf u} \in \mathbb{F}_2^K \}$

-   $\mathrm{rang}(G)=K$ (les lignes de $\mathbf{G}$ sont $K$ mots de
    codes indépendants) et $\mathbf{G}$ non unique.

-   $\mathbf{G}$ est dite systématique si
    $\forall k \in [0,K-1], \exists n \in [0,N-1]$ tel que $c[n]=u[k]$.
    $\mathbf{G}$ peut alors se mettre sous la forme
    $$\mathbf{G}=[P |I_K ]$$
:::
:::

::: frame
### Codes en bloc linéaires

#### Matrice de parité

::: block
Matrice de parité

-   Le code $\mathcal{C}^{\bot}(N-K,K)$, dit code dual, vérifie que tout
    mot du code dual est orthogonal à tout mot du code
    $\mathcal{C}(N,K)$. On note sa matrice génératrice ${\bf H}$.

-   On a alors
    $\{ {\bf c} \in \mathcal{C}(N,K) | {\bf c} \mathbf{H}^{\top} = {\bf 0} \}$

-   Relation avec ${\bf G}$ : ${\bf G}{\bf H}^{\top}={\bf 0}$

-   Pour un code systématique, $\mathbf{H} =[I_{N-K} | P^{\top}]$.

-   Détection d'erreur à l'aide du *syndrome* :
    ${\bf r}={\bf c}+{\bf e}$

    $${\bf s}={\bf r}{\bf H}^{\top}={\bf e}{\bf{H}}^{\top}$$

-   Si ${\bf e}$ est un mot de code, alors on parle d'erreurs *non
    détectable*.
:::
:::

::: frame
### Codes en bloc linéaires

#### Code de Hamming $(N=7, K=4)$

::: center
![image](./Hammingex.png){width="\\textwidth"}
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Introduction

::: block
Définition
$$\mathcal{C}_{H}=\{{\bf c} \in GF(2)^{\times N} | H.\bf{c}^\top = \bf{0}\}$$

-   $H$ est la matrice de parité du code de taille $M \times N$,

-   Si $H$ de rang plein : $R=K/N$ avec $K=N-M$,

-   Equations de parité :
    $\bigoplus_{j: h_{ij}\neq 0} c_j=0, \;\; \forall i=1 \ldots M$,

-   $H$ est dîte à faible densité si
    $$\frac{\mbox{ éléments non nuls }}{N.M} \underset{N \mapsto + \infty}{\longrightarrow} 0$$
:::
:::

::: frame
### Codes LDPC

#### exemple de codes SIRA, N=4096

::: center
![image](./spyLDPC.pdf){width="\\textwidth"}
:::

densité = $0.0017$
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Représentation

::: center
  --------------------------------------- ----------------------------------------
   ![image](./ldpcgen2.pdf){width="45%"}   ![image](./ldpcgen1.pdf){width="50%"}
             Matrice de Parité             Graphe bipartite associé dît de Tanner
  --------------------------------------- ----------------------------------------
:::

::: block

:::
:::

::: frame
### Codes LDPC

#### exemple du code de Hamming

::: center
![image](./Hammingex2.png){width="\\textwidth"}
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes LDPC réguliers

::: block
-   Paramètres : $(d_v,d_c)$,

-   $d_v$ : nombre de $'1'$ par colonne,

-   $d_c$ : nombre de $'1'$ par ligne,

-   $R \geq 1- d_v/d_c$
:::

::: center
  ---------------------------------------
   ![image](./ldpcgen2.pdf){width="45%"}
        Matrice de Parité $(2,d_c)$
  ---------------------------------------
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes LDPC irréguliers

::: block
-   Polynômes associés aux nœuds de variables et de parité :
    $$\begin{array}{cc}
    \lambda(x)=\sum_{i=1}^{d_v}{\lambda_i x^{i-1}} &\rho(x)=\sum_{j=2}^{d_c}{\rho_j x^{j-1}}
    \end{array}$$ avec

    -   $\lambda_i$ : proportion de branches connectées à un nœud de
        variable de degré $i$,

    -   $d_{v}$ : nombre maximum de branches connectées à un nœud de
        variable,

    -   $\rho_j$ : proportion de branches connectées à un nœud de parité
        de degré $j$,

    -   $d_c$ : nombre maximum de branches connectées à un nœud de
        contrainte de parité,

-   Rendement : $$\begin{aligned}
    R \geq 1-\frac{\sum_{j=1}^{d_c}{\rho_j
    /j}}{\sum_{i=1}^{d_v}{\lambda_i / i}}
    \end{aligned}$$
:::
:::

::: frame
### Codes LDPC

#### exemple du code de Hamming

::: center
![image](./Hammingex3.png){width="\\textwidth"}
:::
:::

# Décodage itératif

## Décodage par propagation de croyance {#décodage-par-propagation-de-croyance .unnumbered}

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Décodage par Propagation de croyance (Belief Propagation, BP)

::: block
Décodage itératif des codes LDPC

-   Décodage par Maximum de vraisemblance : trop complexe,

-   Mise en oeuvre d'un algorithme itératif de décodage : algorithme de
    propagation de croyances (Belief Propagation, BP) par mise à jour
    successive de \"messages\" (croyances) en sortie de noeud de
    variables et de parité,

-   Hypothèses : entrelacement parfait\
    $\Rightarrow$ les messages arrivant à un noeud de variable ou de
    parité sont considérés comme indépendants\
    $\Rightarrow$ hypothèse d'**arbre local** qui permet un calcul
    explicite des messages (probabilités ou log-rapport de probabilités
    (LLR)) transitant sur les branches du graphe de Tanner associé,

-   les messages transitant sur le graphe sont par nature
    \"extrinsèques\",

-   Algorithme BP : algorithme itératif sous-optimal à relativement
    faible complexité.
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Décodage par Propagation de croyance

::: center
![image](./LDPCTanner.png){width="50%"}
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Décodage par Propagation de croyance

::: block
Mise à jour des noeuds de variables les messages considérés sont des LLR
$v=\log(\frac{p(c=0| \{ z \})}{p(c=1| \{ z \})})$

::: center
  ------------------------------------------------------------------------------------
                         ![image](./varupdate.pdf){width="60%"}
   $v_m^{(l)}=u_0+\sum_{k=1,k \neq m}^{i}{u_k^{(l-1)}} \mbox{, }\forall m=1 \ldots i$
         $u_0=\log(\frac{p(x=0|y)}{p(x=1|y)})=\log(\frac{p(y|x=0)}{p(y|x=1)})$
  ------------------------------------------------------------------------------------
:::
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Décodage par Propagation de croyance

::: block
Mise à jour des noeuds de parité les messages considérés sont des LLR
$u=log(\frac{p(c'=0|\{ z' \})}{p(c'=1|\{ z' \})})$

::: center
  -----------------------------------------------------------------------------------------------------------------
                                        ![image](./varcheck.pdf){width="50%"}
   $\tanh{\frac{u_k^{(l)}}{2}}=\prod_{m=1,m \neq k}^{j}{\tanh{\frac{v_m^{(l)}}{2}}} \mbox{, }\forall k=1 \ldots j$
  -----------------------------------------------------------------------------------------------------------------
:::
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Décodage par Propagation de croyance

::: block
Décodage et décision
$$v_{\mathrm{app},n}=u_0+\sum_{k=1}^{i}{u_k^{(L)}},\forall n=1 \ldots N$$

$$\hat{m}_n=\frac{1-\mathrm{sign}(v_{\mathrm{app},n})}{2},\forall n=1 \ldots N$$
:::

::: block
Messages initiaux pour différents canaux

-   BEC: $u_0 \in \{ +\infty, -\infty, 0\}$,

-   BSC: $u_0=(-1)^{y[n]} \log(\frac{1-p}{p})$,

-   Gaussien: $u_0=\frac{2}{\sigma_b^2}y[n]$,
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)


::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Comment coder?

::: center
![image](./encoding.png){width="80%"}\
Elimination Gaussienne et permutation de colonnes, complexité $O(n^3)$\
pas la meilleure façon d'aborder le problème
:::
:::

# Familles dérivées

## RA-IRA {#ra-ira .unnumbered}

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes Repeat-Accumulate

::: center
![image](./RAenc.pdf){width="80%"}\
:::

::: block
Principe

-   Prendre $K$ bits, puis les répéter $q$ fois,

-   Entrelacer,

-   coder par un accumulateur de fonction polynôme générateur
    $G_{acc}(D)=1/(1+D)$.
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes Repeat-Accumulate

::: block
Paramètres

-   Rendement :

    -   cas systématique : $R=1/q$,

    -   cas non-systématique : $R=1/(q+1)$.

-   le rendement est limité à 1 ou inférieur à $1/2$.
:::

::: block
Propriétés

-   Structure simple,

-   encdoage linéaire en temps,

-   décodage par BP,

-   bonne performance asymptotique

-   planchers d'erreurs élevés.
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes Repeat-Accumulate

::: center
![image](./TannerRA.pdf){width="50%"}\
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes RA vu comme turbo série

::: center
![image](./RAturbo.pdf){width="70%"}\
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes Irregular Repeat Accumulate

::: block
Structure

::: center
![image](./IRAfamily.pdf){width="70%"}\
:::
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes Irregular Repeat Accumulate

::: block
Principe

-   $k$ bits d'information sont répétés de manière irrégulière,

-   les bits répétés sont *combinés* (combiner),

-   les $m$ bits combinés sont alors encodés par un accumulateur.
:::

::: block
Structure

-   structure IRA classique : $H=[H_u H_p]$, $H_u$ matrice de
    permutation et combinaison
    $$H_p=\left[\begin{array}{ccccc}  1 & & & & (1) \\1 &1 & & & \\ & \ddots & \ddots & & \\ & & 1 &1 \\ & & & 1 &1\end{array}\right]$$
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes Irregular Repeat Accumulate

::: block
Paramètres

-   Rendement (cas systématique):

    $$R=\frac{1}{1+\frac{\overline{q}}{\overline{d}_c}}$$ avec
    $$\overline{q}=\frac{1}{k} \sum_{j}^{k}{d_{b,j}}$$
    $$\overline{d}_c=\frac{1}{m}\sum_{j}^{m}{d_{c,j}}$$

-   Rendement (cas non systématique):
    $R=\frac{\overline{d}_c}{\overline{q}}$
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes IRA: exemple

::: center
![image](./TannerRA.pdf){width="50%"}\
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes IRA vu comme turbo série

::: center
![image](./IRAturbo.pdf){width="70%"}\
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Extensions des codes IRA

::: center
![image](./IRAA.pdf){width="70%"}\
Irregular Repeat Accumulate Accumulate
:::

$$H=\left( \begin{array}{ccc}
 H_u & H_p & 0 \\
 0& \Pi_1^T & H_p 
 
 \end{array}\right)$$
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Extensions des codes IRA

::: center
![image](./ARAfamily.pdf){height="0.55\\textheight"}
:::

::: center
![image](./ARAex.pdf){width="70%"}\
Accumulate Repeat Accumulate
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Extensions des codes IRA

::: center
![image](./GIRA.pdf){width="70%"}\
Generalized Irregular Repeat Accumulate
:::

$$H=[H_u H_p]$$ $$\mbox{Accumulateur} : G(D)=\frac{1}{\sum_i g_i D^i}$$
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Extensions des codes IRA

::: center
![image](./wIRA.pdf){width="80%"}\
Weighted Generalized Irregular Repeat Accumulate
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Low-Density Generator Matrix

::: center
![image](./LDGM.pdf){width="70%" height="0.8\\textheight"}\
LDGM codes
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Low-Density Generator Matrix

::: block
Paramètres

-   On utilise des paramètres différents des codes LDPC: les
    distributions sont calculées sur les branches non connectées à des
    noeuds de variable de degré 1.

-   Rendement :

    $$\begin{aligned}
    R = \frac{\sum_{i=1}^{d_v}{\lambda_i / i}}{\sum_{j=1}^{d_c}{\rho_j
    /j}}
    \end{aligned}$$
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Low-Density Generator Matrix, exemple

::: center
![image](./LDGMex.pdf){height="0.5\\textheight"}\
LDGM codes
:::

$$\lambda(x)=x^2, \rho(x)=\frac{1}{4}+ \frac{1}{2}x + \frac{1}{4} x^2, R= \frac{4}{7}$$
:::

::: frame
### Codes fontaines et Raptors pour la diffusion

Codes Fontaines :

-   Avec $K$ **symboles d'entrée** (info.), l'émetteur génère une suite
    "illimitée" de **symboles de sortie**.

-   Un récepteur peut décoder n'importe quel sous-ensemble de
    $K(1+\epsilon)$ symboles de sortie reçus.

-   Application : transmission multicast.

![image](img/fountainMK.pdf){width="4.5cm"}

![image](shannonoverhead.pdf){width="5.5cm"}

Codes *sans rendement*

-   *Rendement a posteriori*
    ${R_{LT}} \triangleq \frac{\text{\small Nb symb. entrée }}
                {\text{\small Nb symb. sortie nécessaires pour décoder}}$

-   Overhead $\epsilon : R_{LT} (1+\epsilon) = C$ (écart à la capacité)
:::

::: frame
### Codes fontaines et Raptors pour la diffusion

#### Structure

-   code LT caractérisé par une *distribution de degrés de sortie*
    $\Omega (x)=\sum _{i=1}^{d_c} \Omega _i x^i$

-   $\Omega (x)$ est optimisé pour le décodage *itératif*

Génération des symboles codés :

1.  Tirer un degré $d$ selon $\Omega(x)$

2.  Sélectionner $d$ symboles d'entrée de manière uniforme.

3.  Symbole codé émis = XOR des symboles d'entrée

![image](img/raptor2.pdf){width="99%"}

-   Les codes LT atteignent la capacité sur le CBE.

-   Complexité de décodage : $\mathcal{O}(K\log (K))$ pour une
    probabilité arbitrairement faible.

```{=html}
<!-- -->
```
-   Raptor code = précode (code externe) + code LT (code interne,
    rateless),

-   Précode = code correcteur d'erreur de fort rendement,

-   Complexité de décodage : $\mathcal{O}(K)$,

-   Standardisé pour 3GPP-MBMS (codage pour la couche transport) avec
    décodage par élimination Gaussienne sur le BEC.
:::

::: frame
### Codes LDPC généralisés

#### GLDPC (Tanner, 81)

::: center
![image](GLDPC.pdf){width="\\textwidth"}
:::

::: block
-   les contraintes de parités sont des codes linéaires autres que codes
    de parité.
:::
:::

::: frame
### Codes LDPC doublement généralisés

#### DGLDPC (Wang, Paolini, Fossorier)

::: center
![image](DGLDPC.pdf){width="\\textwidth"}
:::

::: block
-   les noeuds de variables sont des codes linéaires autres que noeuds
    de répétitions.
:::
:::

::: frame
### Codes LDPC non binaires

#### Structure des codes LDPC non binaires

::: columns
![image](NBfig1b.jpg){width="6cm"} ![image](NBfig1a.pdf){width="6cm"}
:::

::: block
-   $\mathcal{C}_{H}=\{{\bf x} \in GF(Q)^{\times N} | H.\bf{x}^\top = \bf{0}\}$.

-   $GF(Q) \leftrightarrow \left\{\alpha^k : k= 0 \ldots Q-2\right\}$.

-   Eq. de contraintes :
    $\sum_{j: h_{ij}\neq 0} h_{ij}x_j=0, \;\; \forall i=1 \ldots M$
:::
:::

::: frame
### Codes LDPC non binaire

#### Décodage des codes LDPC non binaires

::: columns
![image](NBBP.pdf){width="7cm" height="5cm"}

-   Noeuds de Variables :
    $$V_m^{(\ell)}= V_0  \prod_{k=0,k \neq m}^{d}{\tilde{U}_k^{(\ell-1)}}$$

-   Permutation :

    $\tilde{V}_m^{(\ell)}=\mathcal{P}_m(V_m^{(\ell)})$

-   Noeuds de Contraintes :
    $$U_k^{(\ell)} = \mathcal{F}^{-1}\left(\prod_{m=1 \ldots d, m \neq k}{\mathcal{F}\left(\tilde{V}_m^{(\ell)}\right)}\right)$$

-   Permutation Inverse :

    $\tilde{U}_k^{(\ell)}=\mathcal{P}_k^{-1}(U_k^{(\ell)})$
:::
:::

::: frame
### Codes LDPC non binaire

#### Décodage des codes LDPC non binaires

-   Noeuds de Variables :
    $$V_m^{(\ell)}= V_0  \prod_{k=0,k \neq m}^{d}{\tilde{U}_k^{(\ell-1)}}, V_0=\left(\begin{array}{c} p(x_j=0 | y_j) \\p(x_j=1 | y_j) \\ p(x_j=\alpha | y_j) \\ \vdots \\ p(x_j=\alpha^{Q-2} | y_j)\end{array} \right)$$

-   Permutation :

    $\tilde{V}_m^{(\ell)}=\mathcal{P}_m(V_m^{(\ell)}) = \left(\begin{array}{c} p(v_m=0) \\p(v_m=\alpha^{Q-2-k+1})\\ \vdots  \\ p(v_m=\alpha^{Q-2})\\ p(v_m=1) \\ \vdots \\ p(v_m=\alpha^{Q-2-k})\end{array} \right)$
:::

::: frame
### Codes LDPC non binaire

#### Décodage des codes LDPC non binaires

-   Noeuds de Contraintes :
    $$\label{eqn:conv_gfq} U_k^{(\ell)} = {\huge \circledast}_{m=1 \ldots d, m \neq k} \tilde{V}_m^{(\ell)}$$

    $$U_k^{(\ell)} = \mathcal{F}^{-1}\left(\prod_{m=1 \ldots d, m \neq k}{\mathcal{F}\left(\tilde{V}_m^{(\ell)}\right)}\right)$$

-   Permutation Inverse :

    $\tilde{U}_k^{(\ell)}=\mathcal{P}_k^{-1}(U_k^{(\ell)})$
:::

::: frame
### Codes LDPC non binaire

#### Décodage des codes LDPC non binaires

::: block
Transformée de Fourier sur un groupe fini Soit $f(.)$ une fonction à
valeurs complexes définie sur le groupe produit $G=(\mathbb{Z}_2^p,+)$,
alors la transformée de Fourier $\hat{f}(.)$ et son inverse sont données
par
$$\hat{f}(\alpha)=\sum_{\beta=0}^{Q-1}{f(\beta)(-1)^{\alpha.\beta^{\top}}}$$

$$f(\alpha)=\frac{1}{2^p}\sum_{\beta=0}^{Q-1}{\hat{f}(\beta)(-1)^{-\alpha.\beta^{\top}}}$$
:::
:::

::: frame
### Modulations codées à bits entrelacés

#### 

::: center
![image](./bicm1.pdf){width="60%" height="0.3\\textheight"}
:::

::: block
Bit-Interleaved Coded Modulation

-   système de transmission à haute efficacité spectrale : constellation
    $M$-aire $\mathcal{S}$ avec $M=2^m$.

-   Peut-être vu comme $\log_2(M)$ canaux parallèle,

-   Capacité atteignable dépend du mapping utilisé :

$$C=m-\frac{1}{2}\sum_{k=0}^{m-1}\sum_{c=0}^{1}{\mathbb{E}\left( \log_2{\left(\frac{\sum_{s_i \in \mathcal{S}}{p(y|s_i)}}{\sum_{s_j \in \mathcal{S}_c^k}{p(y|s_j)}} \right)}\right)}$$
:::
:::

::: frame
### Modulations codées à bits entrelacés

#### 

::: center
![image](./bicmcapavMODAP.pdf){width="80%" height="0.7\\textheight"}
:::
:::

::: frame
### Modulations codées à bits entrelacés

#### 

::: center
![image](./bicmcapavMODAP2.pdf){width="80%" height="0.7\\textheight"}
:::
:::

::: frame
### Démodulation MAP symbole et bit

::: block
Hypothèses

-   Les vecteurs binaires $x[n]=[x_1[n] \cdots x_m[n]]$ sont "mappés\"
    sur des symboles $s[n] \in \mathcal{S}$,

-   Canal sans mémoire à entrées $M$-aires équi-distribués.
:::

::: block
Vraisemblance Symbole et critère MAP associé

-   Symbol Likelihood : $P(y[n]|s[n])$,

-   MAP Symbole :
    $$\hat{s}_n = \mathrm{arg} \max_{s_n}{p(y[n] | s[n]) }$$
:::

::: block
MAP bit

$$\begin{aligned}
L(x_i[n])&= & \log{\left( \frac{\sum_{s[n] \in \mathcal{S}_0^i}{P(y[n]|s[n])P(s[n])}}{\sum_{s[n] \in \mathcal{S}_1^i}{P(y[n]|s[n])P(s[n])}} \right)}\nonumber
\end{aligned}$$
:::
:::

# Codes QC-LDPC

## Codes LDPC quasi-cycliques (QC-LDPC) {#codes-ldpc-quasi-cycliques-qc-ldpc .unnumbered}

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes LDPC Quasi-Cycliques : un exemple

::: center
![image](./codeQC.pdf){width="50%"}\
Matrice de Parité d'un code quasi-cyclique
:::

$\left. \begin{array}{c} \mathbf{c}=[00110|01100|10000|00011] \\
   \mathbf{\tilde{c}}=[00011|00110|01000|10001] \end{array} \right\rbrace \mbox{deux mots de codes possibles}$
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes LDPC Quasi-Cycliques : un exemple

::: center
![image](./spyLDPCQC.pdf){width="75%"}\
Matrice de Parité d'un code quasi-cyclique
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes Quasi-cycliques : définitions et propriétés

::: block
Définitions

1.  chaque mot de code de taille $N=n \times L$ comportent $n$ sections
    de $L$ bits,

2.  toute permutation circulaire des mots de codes restreinte à la
    longueur d'une section est un mot de code.
:::

::: block
Représentation

-   Matrice polynomiale: ces matrices peuvent être représentées par une
    matrice dîte polynomiale dont les éléments sont des polynômes
    associés à la matrice de permutation, $$\tiny P=\begin{pmatrix}
    0 & 1 & 0 & \hdots & \hdots & 0 \\ 
    0 & 0 & 1 & 0 & \ddots  & \vdots \\ 
    \vdots &  &\ddots   & \ddots & \ddots  & \vdots \\ 
    \vdots &  &  & \ddots & 1 & 0 \\ 
    0 &  &  &  & 0 & 1 \\ 
    1 & 0 & \hdots & \hdots & \hdots & 0
    \end{pmatrix}$$
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes Quasi-cycliques : définitions et propriétés

::: block
Exemple : $$H=\begin{pmatrix}
I+P^2 & I+P^4 & I & 0\\  
I+P & P+P^3 & 0 & I
\end{pmatrix}$$
:::

::: block
Définitions

-   Matrice de base : on peut associer à la matrice $H$ une matrice de
    base $H_B$ dont les éléments sont le nombre de monômes à chaque
    éléments non nul de taille $L\times L$,

-   Ordre de lift/extension/expansion : on dît que $H$ est obtenue par
    extension ou "lifting\" de $H_B$ d'ordre $L$.

$$H_B=\begin{pmatrix}
2 & 2 & 1 & 0\\  
2 & 2 & 0 & 1
\end{pmatrix}$$
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes Quasi-cycliques : définitions et propriétés

::: block
Représentation par protographes

-   on peut associer un graphe de Tanner à $H_B$ qui représente la
    description synthétique des connections de $H$,

-   le graphe résultant est appelé protographe (projected-graph),

::: center
![image](./prototest.pdf){width="45%"}\
Représentation du graphe projeté (protographe)
:::
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes Quasi-cycliques : intérêts pratiques

::: block
-   le codage peut être réalisé de manière linéaire en temps car la
    matrice génératrice peut être réalisée à l'aide de simples registres
    à décalage,

-   representation de $H$ simplifiée par utilisation conjointe de la
    matrice de base et des polynômes associés à l'extension,

-   le décodage peut-être réalisé de manière fortement parallélisée

    $\Rightarrow$ codes ayant en général un très bon compromis
    complexité/performance\
    $\Rightarrow$ de facto, le type de codes utilisés dans les standards
:::
:::

# Codes Protographes

## Codes définis par Protographes {#codes-définis-par-protographes .unnumbered}

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes basés protographes : définition

::: block
Définition Protographe = graphe bipartite de petite taille à partir
duquel on construit un graphe plus grand par une procédure dîte de
"copies et permutations"
:::

::: center
![image](./protoseul.pdf){width="40%"}
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes basés protographes : construction

::: block
Etape de copie

1.  le protographe est recopié $L$ fois pour obtenir $L$ répliques.

2.  $L$ est choisi de manière arbitraire pour obtenir la taille de mot
    de code souhaitée $N=n\times L$.
:::

$$\underbrace{\includegraphics[width=0.8\textwidth]{./protocopie}}_{\mbox{L copies}}$$
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes basés protographes : construction

::: block
Etape de permutations

1.  les branches des différentes répliques sont permutées entre les
    différentes répliques,

2.  contrainte de permutation : si un nœud de variable $V_j$ est relié
    avec un nœud de contrainte $C_i$ dans le protographe, le nœud $V_j$
    de chaque réplique ne pourra être connecté qu'à un des $L$ nœuds
    $C_i$ de chaque réplique,
:::

::: block
::: center
![image](./protopermute.pdf){width="80%"}
:::
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes basés Protographes

::: block
::: center
![image](./porotgen.pdf){width="8cm"}\
Représentation complète de la procédure de construction
:::
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes basés Protographes : propriétés

::: block
Propriétés

-   si les permutations sont définies à l'aide de matrices circulantes
    alors ont obtient un code QC-LDPC,

-   le protographe peut être également décrit par sa matrice d'adjacence
    ou matrice de base $H_B$,

    ::: center
    ![image](./protoseul.pdf){width="20%"}
    :::

    $$H_B=\left[ \begin{array}{ccc} 2 &1& 1\\ 1 &1 &1\end{array}\right]$$

-   architecture hautement paralélisable et encodage aisé si QC,

-   codes protographes = codes LDPC dîts structurés
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes basés Protographes

::: block
::: center
![image](./protoeclate.pdf){width="70%"}\
Représentation d'un protographe comme un graphe projeté
:::
:::
:::

# Familles QC dérivées.

## Familles dérivées de codes LDPC  {#familles-dérivées-de-codes-ldpc .unnumbered}

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes Irregular Repeat Accumulate

::: block
Structure

::: center
![image](./IRAfamily.pdf){width="70%"}\
:::
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes Irregular Repeat Accumulate

::: block
Structure

-   structure QC-IRA : $H_{QC}=[H_{u,QC} H_{p,QC}]$
    $$H_{p,QC}=\left[\begin{array}{ccccc}  I & & & & P \\I &I & & & \\ & \ddots & \ddots & & \\ & & I &I \\ & & & I &I\end{array}\right]$$

-   Autre possibilité :
    $$H_{p,QC}=\left[\begin{array}{ccccc}  P & I & & &  \\ &I &I & & \\ I&  & \ddots & \ddots& \\ & &  &I & I\\ P& & &  &I\end{array}\right]$$
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes Irregular Repeat Accumulate

::: block
Standardisation

-   ETSI DVB-S2 : codes LDPC IRA, $N=64800, 16200$.
    $R=1/4, \cdots, 9/10$.

-   IEEE $802.11n$ et $802.16e$ : codes type QC-IRA avec accumulateur
    modifié pour encodage aisé.
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes Accumulate Repeat Accumulate (ARA)

  ------------------------------------------------------------------------
      ![image](./ARAfamily.pdf){width="70%" height="0.5\\textheight"}
   ![image](./araproto.pdf){width="\\textwidth" height="0.4\\textheight"}
  ------------------------------------------------------------------------
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes ARJA (Accumulate Repeat Jagged Accumulate), proposition CCSDS

  -----------------------------------------------------------------
    ![image](./ccsds.jpg){width="70%" height="0.25\\textheight"}
   ![image](./arjaproto.pdf){width="80%" height="0.4\\textheight"}
  -----------------------------------------------------------------
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Codes ARJA : performances

  ----------------------------------------------------------------
   ![image](./arjaperf.pdf){width="90%" height="0.9\\textheight"}
  ----------------------------------------------------------------
:::

# Analyse asymptotique

## Analyse asymptotique et optimisation {#analyse-asymptotique-et-optimisation .unnumbered}

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Analysis et optimisation asymptotique : pourquoi?

::: block
Motivations

1.  Système itératif $\Leftrightarrow$ caractérisation des points fixes,

2.  Prédire les performances asymptotiques pour une famille donnée
    $(\lambda(x),\rho(x))$ et un canal donné,

3.  En deduire des familles "intéressantes\" du point de vue du seuil de
    convergence, ie. approchant la capacité pour une complexité donnée,

4.  une fois la famille sélectionnée, un code peut être construit qui
    hérite de ses performances asymptotiques (sélection d'un candidat
    d'une \"bonne\" famille),

5.  limitations : valable dns le cadre asymptotique seulement.
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Analysis et optimisation asymptotique : cas BEC

::: block
Probabilité d'effacement en sortie d'un noeud de variable

-   Hypothèses : entrelacement parfait (cadre asymtotique),

-   Probabilité d'effacement à la sortie d'un noeud de variable de degré
    $i$ : $$x_v^{(\ell)}(i)=\epsilon (x_c^{(\ell)})^{(i-1)}$$

-   Probabilité d'effacement moyenne à la sortie d'un noeud de variable
    :
    $$x_v^{(\ell)}=\sum_i^{d_v}{\lambda_i x_v^{(\ell)}(i)}=\epsilon \lambda(x_c^{(\ell-1)})$$
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Analysis et optimisation asymptotique : cas BEC

::: block
Probabilité d'effacement à la sortie d'un noeud de variable de parité

-   Probabilité d'effacement à la sortie d'un noeud de parité de degré
    $j$ $$x_c^{(\ell)}(j)=1-(1-x_v^{(\ell)})^{(j-1)}$$

-   Probabilité d'effacement moyenne à la sortie d'un noeud de variable
    :
    $$x_c^{(\ell)}=\sum_i^{d_c}{ \rho_j x_u^{(\ell)}(j)}=1-\rho(1-x_v^{(\ell)})$$
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Analysis et optimisation asymptotique : cas BEC

::: block
Equation d'évolution

$$x_v^{(\ell)}(\epsilon)=\epsilon \lambda(1-\rho(1-x_v^{(\ell-1)}))=F(\epsilon, x_v^{(\ell-1)})$$

-   $F(\epsilon, x)$ fonction croissante de $x$ et $\epsilon$,

-   Monotonicité par rapport au paramètre de canal :

    $$\mbox{Si } x_v^{(\ell)}(\epsilon) \underset{ \ell \to +\infty}{\longrightarrow} 0, \; \mbox{alors } x_v^{(\ell)}(\epsilon') \underset{ \ell \to +\infty}{\longrightarrow} 0, \;\; \forall 0 \leq \epsilon' \leq \epsilon$$

-   Convergence vers un point fixe dans $[0,\epsilon]$, solution de
    $$F(\epsilon, x)=x$$
:::

::: block
Notion de seuil de convergence ("threshold\")
$$\epsilon^{*}= \sup_{\epsilon}{\{x_v^{(\ell)}(\epsilon) \underset{ \ell \to +\infty}{\longrightarrow} 0\}}$$
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Analysis et optimisation asymptotique : cas BEC

::: block
Condition de stabilité Pour le point fixe $x_v=0$, les distributions de
degrés doivent vérifiées: $$\epsilon \lambda'(0)\rho'(1) <1$$
:::

::: block
Optimisation d'une séquence pour $\rho(x)$ fixé (notation vectorielle)
$$\underline{\lambda}_{opt}=\max_{\underline{
\lambda }}{\underline{1/d_v}^{\top} \underline{ \lambda }}$$ sous les
contraintes :

-   Contrainte de mélange :
    $\underline{ \lambda }^{\top}\underline{1}=1$

-   Contrainte de proportion :
    $\lambda_i \in [0,1], \;\; \forall i=2 \ldots d_v$

-   Contrainte de convergence :
    $\mathrm{F}\left(\underline{\lambda},x,\frac{2}{\sigma^2} \right) < x, \; \forall x \in [0,1]$

-   Condition de stabilité :
    $\lambda_2 < \frac{1}{\epsilon \; \sum_{j=2}^{d_c}{\rho_j(j-1)}}$
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Analysis et optimisation asymptotique : cas Gaussien

::: block
Canal Gaussien : approximation Gaussienne

-   les messages log- rapports de vraisemblance du décodeur sont
    considérés comme Gaussiens consistents:
    $$x \sim \mathcal{N}(\pm m,2m)$$

-   Fonction d'information mutuelle $J(.)$ :
    $$J(m)=1-\mathbb{E}_x(\log_2(1+e^{-x})), \;\; x \sim \mathcal{N}(+m,2m)$$
:::

::: block
Modélisation à la sortie d'un noeud de variable

$$x_{v}^{(\ell)}=\sum_{i=2}^{d_v}{\lambda_i\textrm{J}(\frac{2}{\sigma^2}+(i-1)\textrm{J}^{-1}(x_{c}^{(\ell-1)}))}$$
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Analysis et optimisation asymptotique : cas Gaussien

::: block
Modélisation à la sortie d'un noeud de parité

-   "Reciprocal channel approximation" pour noeud de parité de degré
    $j$:
    $$x_c^{(\ell)}(j)= 1-J\left((j-1) J^{-1}\left(1-x_v^{(\ell-1)}\right)\right)$$

-   Information mutuelle moyenne en sortie de noeud de parité :
    $$x_c^{(\ell)}=1-\sum_j{\rho_j J\left((j-1) J^{-1}\left(1-x_v^{(\ell-1)}\right)\right)}$$
:::

::: block
Seuil de convergence ("threshold\")
$$x_{v}^{(l)}=F(\lambda(x), \rho(x),x_{v}^{(l-1)},\sigma^2)$$
$$\begin{aligned}
\delta^{*}&=&
\min_{\sigma^2}{\{\frac{1}{2R\sigma^2}|F(\lambda(x), \rho(x),x_v,\sigma^2)>x_v
, \;\forall x_v \in [0,1]\}}
\end{aligned}$$
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

::: block
Condition de stabilité Pour le point fixe $x_v=1$, les distributions de
degrés doivent vérifier:
$$\lambda'(0)\rho'(1) < \exp{(\frac{1}{2 \sigma^2})}$$
:::

::: block
Optimisation d'une séquence pour $\rho(x)$ fixé (notations vectorielles)
$$\underline{\lambda}_{opt}=\max_{\underline{
\lambda }}{\underline{1/d_v}^{\top} \underline{ \lambda }}$$ sous les
contraintes :

-   Contrainte de mélange :
    $\underline{ \lambda }^{\top}\underline{1}=1$

-   Contrainte de proportion :
    $\lambda_i \in [0,1], \; \forall i=2 \ldots d_v$

-   Contrainte de convergence :
    $\mathrm{F}\left(\underline{\lambda},x,\frac{2}{\sigma^2} \right) > x, \; \forall x \in [0,1]$

-   Condition de stabilité :
    $\lambda_2 < \frac{1}{\sum_{j=2}^{d_c}{\rho_j(j-1)}} e^{\frac{1}{2 \sigma^2}}$
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Analysis et optimisation asymptotique

::: block
Propriétés de l'air sous EXIT charts Soit un système concaténé série,
alors pour le BEC:

$$\mathcal{A}_1=\int_{0}^{1}{I_{E_1}(I_{A_1})dI_{A_1}}=1-R_1$$

$$\mathcal{A}_2=\int_{0}^{1}{I_{E_2}(I_{A_2})dI_{A_2}}=\frac{I(\overline{X},\overline{Y})}{n R_2}$$

$$R_1 R_2 < \frac{I(\overline{X},\overline{Y})}{n} \leq C$$
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### EXIT chart multidimensionnelles (PEXIT)

::: block
Motivations

-   Etendre l'analyse EXIT au cas des codes structurés.

-   Approche PEXIT qui utilise la matrice de base du protographe pour
    analyser son seuil de convergence.

-   idée : traquer l'information mutuelle de manière détaillée en
    fonction de la topologie locales des noeuds.
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### EXIT chart multidimensionnelles (PEXIT)

-   Soit $h_{ij}$, le coefficient de $H_{B}$ à la ligne $i$ et à la
    colonne $j$,

-   A l'itération de décodage $\ell$, on utilisera les notations
    suivantes:

    -   $x_{cv}^{(\ell)}(i,j)$ : information mutuelle moyenne entre le
        message (LLR) envoyé par un nœud de parité $C_i$ au de variable
        $V_j$ et le bit associé du mot de code, information portée par
        une des $h_{i,j}$ branches qui connecte $C_i$ à $V_j$,

    -   $x_{vc}^{(\ell)}(i,j)$ : information mutuelle moyenne entre le
        message (LLR) envoyé par un nœud de variable $V_j$ au nœud de
        parité $C_i$ et le bit associé du mot de code, information
        portée par une des $h_{i,j}$ branches qui connecte $V_j$ à
        $C_i$,

    -   $x_{app}^{(\ell)}(j)$ : information mutuelle moyenne entre le
        LLR bit a posteriori évalué au nœud $V_j$ et le bit de mot de
        code associé.

-   LLR canal associé au nœud de variable $j$ :
    $m_{ch,j} =2/\sigma _{b,i}^{2}$ où $\sigma _{b,i}^{2}$ est la
    variance du canal vu par le nœud $j$.

-   Si nœud de variable $j$ poinçonné, $m_{ch,j} =0$.
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### EXIT chart multidimensionnelles

-   **Mise à jour des nœuds de variables :**

    $\forall j=0\cdots n-1{\kern 1pt} \; et\; \forall i=0\cdots m-1{\kern 1pt}$

    -   si $h_{ij} =0$, $x_{vc}^{(\ell)}(i,j)=0$.

    -   sinon

        $$x_{vc}^{(\ell)} (i,j)=J\left(\sum _{k\ne i} h_{kj} J^{-1} (x_{cv}^{(\ell-1)} (k,j))+(h_{ij} -1)J^{-1} (x_{cv}^{(\ell-1)} (i,j))+m_{ch,j} \right)$$

-   **Mise à jour des nœuds de contraintes de parité :**

    $\forall i=0\cdots m-1{\kern 1pt} \; et\; {\kern 1pt} \forall i=0\cdots n-1$

    -   si $h_{ij} =0$, $x_{cv}(i,j)=0$.

    -   sinon

        $$x_{cv}^{(\ell)} (i,j)=1-J\left(\sum _{k\ne j} h_{ik} J^{-1} (1-x_{vc}^{(\ell)} (i,k))+(h_{ij} -1)J^{-1} (1-x_{vc}^{(\ell)} (i,j))\right)$$
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### EXIT chart multidimensionnelles

-   **Calcul de de l'information mutuelle a posteriori par nœud de
    variable:**

    $$\forall j=0\cdots n-1{\kern 1pt} ,\; {\kern 1pt} x_{app}^{(\ell)} (j)=J\left(\sum _{k} h_{kj} J^{-1} (x_{cv}^{(\ell)} (k,j))+m_{ch,j} \right)$$

::: block
-   La convergence est obtenue si $x_{app}^{(\ell)} (j)=1\; \forall j$.

-   Cette analyse permet de calculer pour un protographe donné son seuil
    de convergence, permettant ainsi de comparer les performances entre
    différentes familles de codes protographes.
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Analysis et optimisation asymptotique : EXIT charts

::: center
![image](./exitldpc.pdf)
:::
:::

# Construction de codes à taille finie

## PEG {#peg .unnumbered}

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Enumérateurs pour codes RA

::: center
![image](./SCC.pdf){width="80%"}
:::

::: block
Enumérateurs entrée-sortie pour système concaténé série (SCC)
$$A_{i,w}^{SCC}=\sum_{d=d^1_min}^{K_2}{\frac{A^{C_1}_{i,d}. A^{C_2}_{d,w}}{\displaystyle\binom{K_2}{d}}}$$
:::

::: block
Enumérateurs entrée-sortie pour code RA
$$A_{i,w}^{RA}=\sum_{d=q}^{qK}{\frac{A^{rep}_{i,d} . A^{acc}_{d,w}}{\displaystyle\binom{qK}{qi}}}$$
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Enumérateurs pour codes RA

::: block
Enumérateurs entrée-sortie pour code RA

$$A^{rep}_{i,d} = \displaystyle\binom{K}{i} \delta(d-qi)$$

$$A^{acc}_{d,w} = \displaystyle\binom{m-w}{\lfloor d/2 \rfloor} \displaystyle\binom{w-1}{\lceil d/2\rceil-1}$$

$$A_{i,w}^{RA}=\sum_{d=q}^{qK}{\displaystyle\binom{K}{i} \displaystyle\binom{qK-w}{\lfloor qi/2 \rfloor} \displaystyle\binom{w-1}{\lceil qi/2\rceil-1}}{\displaystyle\binom{qK}{qi}}$$

$$P_b < \frac{1}{K} \sum_{w=w_{\min}}^{qK} \sum_{i=i_{\min}}^{K}{i A_{i,w}^{RA} \exp{(-wRE_b/N_0)}}$$
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Points fixes du décodeur, cas du BEC

  ------------------------------------------------------------- ------------------------------------------------------------
   ![image](./SSDef.pdf){width="50%" height="0.3\\textheight"}   ![image](./SSex.pdf){width="50%" height="0.9\\textheight"}
  ------------------------------------------------------------- ------------------------------------------------------------
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### PEG algorithm

![image](./PEG1.pdf){width="80%" height="0.7\\textheight"}
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### PEG algorithm

![image](./PEG2.pdf){width="80%" height="0.7\\textheight"}
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Performances asymptotiques

::: center
![image](./ldpc_perf1.pdf){width="\\textwidth"}
:::
:::

::: frame
### Codes Low-Density Parity-Check (LDPC)

#### Performances

::: center
![image](./ldpc_perf2.pdf){width="\\textwidth"}
:::
:::

::: frame
### Bibliographie

-   W.E. Ryan, Shu Lin, *Channel codes: classical and modern*, Cambridge
    University Press, 2009.

-   T. Richardson, R. Urbanke, *Modern coding theory*, Cambridge
    University Press, 2008.

-   S.J. Johnson, *Iterative Error Correction: Turbo, Low-Density
    Parity-Check and Repeat-Accumulate Codes*, Cambridge University
    Press, 2010.

-   Todd K. Moon, Error Control Coding: Mathematical Methods and
    Algorithms, Wiley, 2005.
:::
