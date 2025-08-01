![[ML Non Supervisionato2.jpg|700]]

### [[clustering]]
L'analisi dei cluster (cluster analysis) è una tecnica statistica multivariata il cui obiettivo è raggruppare oggetti in base a un insieme di caratteristiche selezionate dall'utente.
L'analisi dei cluster consente di dividere un insieme di osservazioni in cluster (sottoinsiemi) in modo tale che:
➢ le ==osservazioni simili ==(o correlate) tra loro si trovano nello stesso gruppo
➢ le ==osservazioni dissimili== (o non correlate) rispetto agli oggetti si trovano in altri gruppi

Ogni gruppo contiene una serie di elementi disgiunti. Esistono due diverse tipologie di clustering:
	•[[Hard-Clustering]], ciascun data-item xi appartiene ad un solo cluster Cj, quindi i cluster sono mutuamente esclusivi;
	•[[Soft-Clustering]], ciascun data-item ha un grado di appartenenza (γki) ad un cluster. in cui γki rappresenta il grado di appartenenza del punto i. Questo è tipicamente associato ad un modello probabilistico: più alto è γki, più alta è la probabilità che il punto i appartenga al cluster k.

### Come Funziona la Cluster Analysis? 
Passaggi Principali:
➢ Selezione delle Caratteristiche: Si scelgono le variabili o caratteristiche da analizzare, ad esempio età + glicemia + BMI + ….
➢ *Calcolo della Similarità/dissimilarità*: Si misura la similarità tra le osservazioni usando ==metriche come la distanza euclidea== utilizzando una funzione di dissimilarità, per scoprire quanto siano dissimili l’uno dall’altro, oltre ad una funzione di perdita/costo che consenta di valutare i vari cluster, e un algoritmo per ottimizzare la funzione di perdita/costo.
➢  *Algoritmo di Clustering:* Si applica un algoritmo per ==dividere i dati in cluster.== 
	Una caratteristica degli algoritmi di clustering è quella di avere molte e diverse funzioni di costo (probabilistiche o non), e ciascuna di esse caratterizza l’algoritmo di clustering. Avendo a disposizione un dataset D quello che il clustering cerca di fare è andare a definire un numero k di insiemi disgiunti che rappresentano le caratteristiche peculiari del dataset, e per questo si tratta di un algoritmo che aiuta a fare ==Data Exploration==, ad esplorare e comprendere l’insieme dei dati che si hanno a disposizione

![[Pasted image 20250528215511.png]]

### METODI DI CLUSTERING
➢ [[Kmeans]]: ==è un metodo che raggruppa i punti dati in un numero predefinito a priori (k) di cluster basato sulla loro distanza dal centroide di ciascun cluster. Si tratta di un algoritmo iterative.==
➢ [[Clustering Gerarchico]]: ==è un metodo che crea una gerarchia di cluster suddividendoli o unendoli ricorsivamente in base alle loro somiglianze.==


Una delle diverse tipologie di [[ML Non Supervisionato]] è la Principal Components Analysis ([[PCA]])
