
![[Cluster Gerarchico_Dettaglio.png]]Il Clustering Gerarchico Agglomerativo è una tecnica di clustering utilizzata per organizzare i dati in una struttura ad albero, chiamata dendrogramma, che rappresenta le relazioni di similarità tra i dati.

Caratteristiche principali:
- **Agglomerativo**: si considera ciascun data item come un cluster individuale, e ad ogni passo si uniscono le coppie di cluster che sono più vicine, finché non si trova un unico cluster, o il numero k di cluster che si vogliono considerare;
- **Divisivo**: si parte da un unico cluster inclusivo di tutti i data item e ad ogni passo si elimina da ogni cluster il punto più distante finché ogni cluster contiene un solo data point, o si identificano k cluster.

➢ Distanza e Similarità: La fusione tra cluster è basata su una misura di distanza, come la distanza Euclidea o Manhattan, o su una misura di similarità.
➢ Dendrogramma: La struttura gerarchica creata aiuta a visualizzare i cluster e a scegliere il numero ottimale di gruppi.

Le distanze che possono essere utilizzate in un algoritmo di cluster gerarchico sono:
**Single Linkage (Collegamento Singolo):** calcola la distanza minima tra i punti di due cluster. La distanza tra due cluster è data dalla distanza più breve tra i singoli punti in ciascun cluster. È sensibile al rumore e tende a formare cluster "a catena".
**Complete Linkage (Collegamento Completo):** calcola la distanza massima tra i punti di due cluster. La distanza tra due cluster è quindi data dalla distanza maggiore tra i punti nei due cluster. Questo metodo tende a creare cluster più compatti e di forma simile.
**Average Linkage (Collegamento Medio):** misura la distanza media tra tutti i punti di un cluster e tutti i punti di un altro cluster. Spesso è una scelta bilanciata per ottenere cluster di forma uniforme.
**Centroid Linkage (Collegamento del Centroid):** calcola la distanza tra i centroidi (o medie) di ciascun cluster. È sensibile alle variazioni nei centroidi e funziona bene se i cluster hanno distribuzioni simmetriche.

![[Pasted image 20250529232504.png]]

