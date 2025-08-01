Dati due vettori di elementi xi e yi, con i= 1, . . . , n si vuole apprendere una ==funzione== f : **X** →Y che permette ottenere Y a partire da X, dove:
 • ==X== è il vettore degli attributi di input, altrimenti noti come ==features;==
•==Y== è il vettore delle ==labels==, che si vuole andare ad ottenere come output dell’algoritmo;
- *[[Classificazione]]
	- Nel caso di Y che contiene dati ==categorici e/o qualitativi==, quindi appartenenti ad un ==dominio discreto (numerico o tipicamente testuale)==, si parla di Problemi di Classificazione; richiede campioni di riferimento precedentemente classificati (a priori) per addestrare il classificatore e successivamente classificare i dati sconosciuti
- *[[Regressione]]
	- Se Y è un vettore rappresentato da dati puramente numerici e/o quantitativi in ==dominio continuo==

Importante è comprendere i metodi con cui si muove il dominio del ML supervisionato. Esistono:
	•[[Metodi parametrici]], in cui si definisce la forma funzionale della funzione f (X) e si cerca il modello che meglio si adatta ai dati;
	•[[Metodi non parametrici]] in cui si cerca la miglior funzione f (X) che si adatta ai dati, senza però dare alcuna assunzione a priori circa il tipo o la forma della funzione f (X) stessa *(Un esempio di un metodo non parametrico è il metodo dei ==K-Nearest Neighbors==, nel quale si trovano i punti che appartengono ad una certa tipologia di classificazione andando ad identificare i punti di quella classifica che sono più vicini al punto stesso. Si fanno considerazioni indipendenti dalla definizione di una funzione, ma caratterizzate solo dalla presenza di quel punto in un certo spazio e da ciò che esso ha intorno in termini di caratterizzazione del vettore Y)*

> [!important] Mean Squared Error (MSE)
> E’ essenziale considerare che, quando si trova la funzione f (X) che permette di ottenere, a partire dal vettore X il vettore delle labels Y questo lo si fa con un ==errore ε dovuto all’approssimazione (Y= f (X) + ε)==. In questi casi bisognerà valutare il modello usando una metodologia, quale ad esempio la ==Mean Squared Error (MSE)==


Per verificare la validità di questi algoritmi si va a dividere il dataset completo in un [[dataset di training ]](80%) e un [[dataset di test]] (20%): si fa girare il modello cercando quali siano i parametri migliori sul dataset di training, e poi lo si applica su quello di test per verificare che i parametri prima applicati siano ancora applicabili e portino i risultati desiderati.