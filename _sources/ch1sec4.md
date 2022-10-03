## Théorème du codage canal

```{prf:theorem}

Pour un canal à temps discret, il est possible de transmettre de l'information avec une probabilité d'erreur arbitrairement faible si le
débit de communication $R$ est inférieur à la capacité du canal, i.e. $R < C$. 

Plus précisément, pour tout $R < C$, il existe une séquence de schémas de codage de longueur $N$ de probabilité d'erreur moyenne
$P_e^(N)$ tendant vers zéro quand $N \longmapsto +\infty$

Inversement, toute séquence de schémas de codage avec une probabilité d'erreur tendant veers zéro doit vérifier $R<C.$ Si $R>C,$ la
probabilité d'erreur est forcément non nulle.
```

La capacité représente donc la quantité d'informations qui peut être transmise de manière *fiable* à travers un canal par utilisation de
canal. Pour $R>C,$ aucune communications fiable, sans erreur n'est possible.

Dans le cas d'un canal AWGN, on aura quelques remarques intéressantes à faire sur cette relation. Par le théorème précédent, on aura

$$\begin{aligned}
R &< C_{AWGN} \\
&= \log_2(1+\frac{E_s}{2\sigma^2})\\
&= \log_2(1+\frac{E_s}{N_0})\\
&= \log_2(1 + R \frac{E_b}{N_0})
\end{aligned}$$

où $E_b$ est l'énergie par bit utile/d'information. On a alors

$$\frac{E_{b}}{N_{0}}>\frac{2^{R}-1}{R} \underset{R \to 0}{\longrightarrow}  \ln(2)=-1.59 dB$$
