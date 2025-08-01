Un altro indice utilizzato che offre un’indicazione più concreta sul numero di cluster k da considerare è l’Indice di Davies-Bouldin: si effettua la media delle distanze $D_{i}$ , rappresentate dal massimo del rapporto tra la separazione interna al cluster i e il cluster j ($S_{i}$ e $S_{j}$), rispetto alla separazione tra il cluster i e il cluster j ($M_{i,j}$). L’indice DB non fa altro che trovare la media di tutti i massimi, andando quindi a rappresentare la situazione di scattering interno (tra i vari cluster) e lo scattering tra coppie di cluster. In formula:

${\displaystyle R_{i,j}={\frac {S_{i}+S_{j}}{M_{i,j}}}}$

 ${\displaystyle D_{i}\equiv \max _{j\neq i}R_{i,j}}$

If N is the number of clusters:

 ${\displaystyle {\mathit {DB}}\equiv {\frac {1}{N}}\displaystyle \sum _{i=1}^{N}D_{i}}$
 