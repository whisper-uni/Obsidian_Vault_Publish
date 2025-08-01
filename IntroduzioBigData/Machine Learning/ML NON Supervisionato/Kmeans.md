![[Dettaglio K-means.png]]


L'obiettivo che l'algoritmo si prepone è di minimizzare la varianza totale intra-gruppo; ogni gruppo viene identificato mediante un centroide $\mu_K$ o punto medio. 

L'algoritmo  divide datset composto da N misure (o osservazioni) (x1,x2...xn)   in K clusters (gruppi) con N>> K seguendo una procedura iterativa: 
1. Scegliere il numero di cluster k che si vogliono trovare;
2. Generare k punti casuali come centroidi $\mu_K$  di ciascun cluster (rappresentativi del centro di ciascun cluster);
3. [[#Evaluation-step (E-step)]]: Assegnare ciascun data point al centroide del cluster più vicino (in termini di distanza utilizzando una [[#Funzione di similarità]]);
4. [[#Minimization-step (M-step)]]: Ricalcolare il nuovo centroide del cluster;
5. [[#Loop di Evaluation-step (E-step) e Minimization-step (M-step)]] Ripetere il passo 3 e 4 finché non si converge
###### Funzione di similarità
La funzione più semplice è la [[Distanza]] : più un elemento è distante, più è dissimile da un altro, più è vicino più è simile. Di solito si utilizza la [[Distanza#distanza euclidea 2-distanza = ${ sqrt { sum _{i=1} {n} x_{i}-y_{i} {2}}}$|distanza euclidea]] (*bisogna considerare che i dati devono essere scalati, quindi omogenei dal punto di vista della distanza: possono esserci dati che hanno unità di misura diverse le une dalle altre, quindi potrebbero aversi fattori di
distanza più o meno significativi; quindi si ricorre ad una normalizzazione dei dati di input..*)

###### Funzione obiettivo/costo

La funzione obiettivo del K-Means, che l'algoritmo cerca di minimizzare iterativamente, è la **Somma dei Quadrati all'interno dei Cluster (Within-Cluster Sum of Squares - WCSS)**, a volte chiamata anche "inerzia". La sua formula è:

$J=\sum_{i=0}^{n}||x_i - \mu_j||^2$

Questa funzione J viene ad essere minimizzata nei  passi successivi:

 ###### Evaluation-step (E-step):
 - per ogni punto dati nel dataset, l'algoritmo calcola la [[Distanza#distanza euclidea 2-distanza = ${ sqrt { sum _{i=1} {n} x_{i}-y_{i} {2}}}$|distanza euclidea]]  tra quel punto e _ogni_ centroide esistente.
- Il punto viene poi assegnato al cluster il cui centroide risulta essere il **più vicino** (quello con la distanza minima). Questa è   una decisione "greedy" (locale) per ogni singolo punto. Quindi  fissato il centroide µk si minimizza J  assegnando ciascun data item al suo centroide più vicino
		   
 ###### Minimization-step (M-step):
 
 fissata l’assegnazione dei data item ai centroide nel passo precedente, si effettua una nuova minimizzazione di J ricentrando µk in modo tale che ciascun centroide venga ad essere la media dei punti che appartengono al cluster K (crea nuovi centroidi prendendo il valore medio di tutti i campioni assegnati a ciascun centroide precedente.) 

- Una volta che tutti i punti sono stati assegnati a un cluster, l'algoritmo ricalcola la posizione di ciascun centroide. Il nuovo centroide di un cluster è la **media (o baricentro)** di tutti i punti che sono stati assegnati a quel cluster.
- in questa fase che si vede la connessione con la [[#Funzione obiettivo/costo]]: si può dimostrare matematicamente che il centroide calcolato come media dei punti di un cluster è la posizione che minimizza la somma dei quadrati delle distanze dei punti _a quel centroide specifico_.
 
 ###### Loop di [[#Evaluation-step (E-step)]] e [[#Minimization-step (M-step)]]
Questa procedura viene ripetuta ciclicamente fino a convergere, sempre e comunque, ad un minimo locale. 
$\sum_{i=0}^{n}\min_{\mu_j \in C}(||x_i - \mu_j||^2)$

**In sintesi:**

- **Assegnazione dei punti:** Avviene misurando la [[Distanza#distanza euclidea 2-distanza = ${ sqrt { sum _{i=1} {n} x_{i}-y_{i} {2}}}$|distanza euclidea]]  (con la radice quadrata) di ciascun punto da ogni centroide e assegnando il punto al centroide che restituisce la distanza minima.
- **Minimizzazione della funzione obiettivo:** La funzione obiettivo (WCSS, Somma dei Quadrati all'interno dei Cluster, che usa la distanza Euclidea _al quadrato_) viene minimizzata **indirettamente** attraverso l'alternanza di queste due fasi. Ogni passo (sia l'assegnazione che il ricalcolo dei centroidi) garantisce che il valore della WCSS non aumenti, e tipicamente diminuisca, portando l'algoritmo verso un minimo locale della funzione obiettivo.

Questo fa si che si riesca a garantire la convergenza in un numero finito di passi. I punti iniziali vengono scelti in maniera euristica, casuale: l’idea è quella di scegliere il centroide i+-esimo in modo da essere più possibile lontano dai primi. I limiti di questa scelta sono dati dai limiti spaziali dei data points nelle n dimensioni che abbiamo a disposizione.




Altro aspetto fondamentale è quello di scegliere il numero k di cluster:

- ###### [[Elbow criteria]]
- ####### [[Indice di Davies-Bouldin]]
