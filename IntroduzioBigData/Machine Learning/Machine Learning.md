il ML è l’integrazione di differenti tecniche allo scopo di estrarre valore dai dati. 

 [[ML Supervisionato]]
	-Dato un insieme di dati si vuole andare a scegliere la funzione che meglio approssima l’insieme dei dati considerato, avendo però come input la tipologia di funzione e la classe di funzione che si va a considerare.
	
[[ML Non Supervisionato]]
	Dato l’insieme dei dati xi, con i= 1, . . . , n si vuole inferire la struttura intrinseca della matrice o del vettore X. Questa tecnica è utilizzata tipicamente per fare ==analisi esplorativa dei dati==, poiché non si attribuisce alcuna *classificazione*, piuttosto che nessun valore atteso Y su cui costruire la funzione f (X); semplicemente si caratterizza in gruppi omogenei il dataset di input.Il ML Non Supervisionato presenta dei limiti: oggettivamente non ha uno scopo singolo e specifico e ==non si conosce a priori il numero di cluster== in cui dividere il dataset *(si decide soggettivamente in quanti cluster suddivider il dataset); inoltre non c’è modo di fare verifiche incrociate (Nel ML Supervisionato si divideva in dataset in un training dataset e in un test dataset, e si verificava che il modello applicato al training dataset fosse valido per il test dataset. Nel caso ML Non Supervisionato questo non è più valido: dato un dataset si identificano i cluster)* di cui si compone, ma se cambia il dataset cambiano anche i cluster.)
	[[ML Non Supervisionato#clustering|clustering]]
	*[[PCA]]
[[Deep Learning]]
