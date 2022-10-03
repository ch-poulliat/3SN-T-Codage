






### Représentation en treillis des codes en bloc

Pour pouvoir décoder efficacement un code en bloc au sens du maximum de
vraisemblance sans passer par une énumération à complexité prohibitive,
on peut dériver une représentation graphique appelée *treillis* qui
permet de représenter efficacement la structure sous-jacente des mots de
codes. Plusieurs types de treillis peuvent être définis pour un code en
bloc, parmi les plus utilisé, on peut citer le treillis associé à la
matrice de parité. En partant de l'équation
$\mathbf{cH}^{\mathrm{T}}=\mathbf{0},$ où $\mathbf{H}$ est la matrice de
parité de taille $M \times N.$ En notant $\mathbf{h}_{j}$ la $j$-ième
colonne de $\mathbf{H}$, on obtient l'équation vectorielle
$$c_{1} \mathbf{h}_{1}+c_{2} \mathbf{h}_{2}+\cdots+c_{n} \mathbf{h}_{n}=\mathbf{0}.$$

On peut alors définir une représentation dans l'\"espace des états\" où
l'état $S_{\ell}$ correspond à la somme partielle des colonnes
$\mathbf{h}_j, \; j=1 \cdots \ell$ défini comme suit
$$S_{\ell}=c_{1} \mathbf{h}_{1}+c_{2} \mathbf{h}_{2}+\cdots+c_{\ell} \mathbf{h}_{\ell}$$
Par convention, on a $S_{0}=S_{N}=\mathbf{0},$ ie. on commence par un
vecteur 'somme partielle' nul et par définition de l'équation de parité,
la somme totale des colonnes est nulle. De plus, comme $\mathbf{h}_{j}$
sont des vecteurs appartenant à $\mathbb{Z}_2^M$, le nombre d'états
maximum est de $2^{m}$ pour chaque somme partielle
$\ell=1,2, \ldots, N-1.$ Cette description du code dans l'espace des
états $S_{\ell}$ donne une représentation graphique de type treillis
dont la structure permet d'énumérer efficacement les mots de code,
chaque chemin représentant un mot de code possible. Contrairement au cas
des codes convolutifs, comme nous le reverrons dans le chapitre suivant,
ce treillis varient dans le temps. Son application dépend également du
rendement du code. En effet la complexité pour le décodage ML sera de
l'ordre de $\mathcal{O}(2^M).$ Ainsi cette méthode sera intéressante
pour des rendements élevés ($M$ \"petit\"). Quand le rendement diminue,
on préferra une représentation par un treillis donné par la matrice
génératrice ou en utilisant le code dual.



# Codes convolutifs : structure et décodage








# Concaténation de codes en treillis




# Analyse asymptotique : EXIT charts

Le but de ce chapitre est d'intriduire l'analyse de performance des
schéma turbo dans le cadre dît asymptotique, ie. les performances de ces
schémas quand la raille des mots de codes tend vers l'infini. Le but est
de prévoir ce que l'on nomme le seuil de décodage de ces schémas à
savoir le point d'opération en $E_b/N_0$ minimum pour lequel on peut
garantir une convergence du schéma itératif vers une propabilité
d'erreur arbitrairement petite. En dessous de ce seuil, la probabilité
d'erreur sera alors nécessairement non nulle. Ce type d'analyse permet
dès lors de prédire les performances du schéma de sélectionner/optimiser
les schémas de codage basés sur des concaténations parallèles ou série.
De la même façon on pourra alors prédire les performances en fonction du
rapport signal à bruit.

### Présentation générale

Une courbe EXIT (*EXIT chart*) sert à analyser le comportement
entrée-sortie d'un bloc à entrées et sorties souples (SISO). On cherche
ainsi à déterminer une relation entrée-sortie pour caractériser un bloc
de décodage suivant une figure de mérite donnée. Le bloc opérant sur des
entrées homogènes à des probabilitès/vraisemblance ou versions log, on
caractérisera donc se comportement *en moyenne*. Dans le cas générale,
un bloc SISO dépend en entrées du canal (via les observations issues du
canal) et de l'a priori (donné par les informations extrinsèques d'un
autre bloc SISO). En sortie, on a alors deux sorties, l'une liée à
l'information extinsèque, l'autre liée à information a posteriori. Le
but d'une courbe EXIT est de modéliser de manière indépendante chaque
bloc SISO de la chaîne. Pour ce faire si on peut *mesurer* un certaine
quantité en sortie en fonction des paramètres moyens d'entrée, on se
doit de définir un modèle statistique a priori pour l'information
extrinsèque en entrée du bloc SISO, les données observées et donc
simulées suivant elles le modèle de canal prédéfini.

Pour simplifier l'analyse et dans certains cas la mise en équations des
processus de décodage, on voudra caractériser chaque bloc par une
relation entrée-sortie mono-dimensionnelle de type
$\mathrm{Output}=F(\mathrm{SNR},\mathrm{Input})$. La figure de mérite
$\mathrm{Input}$ en entrée sera associée aux informations a priori
entrantes (extrinsèques des autres blocs), de même, la figure de mérite
sortante $\mathrm{Output}$ sera associée aux informations extrinsèques
fournies par le bloc SIS0
