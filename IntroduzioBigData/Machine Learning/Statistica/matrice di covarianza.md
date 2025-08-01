Calcolo della [[matrice di covarianza]] di X: S
La matrice di covarianza è una matrice simmetrica _p_ × _p (dove p_ è il numero di dimensioni) che ha come voci le covarianze associate a tutte le possibili coppie delle variabili iniziali. Ad esempio, per un set di dati tridimensionale con 3 variabili _x_ , _y_ e _z_ , la matrice di covarianza è una matrice 3 × 3 di questo da:

  
![Analisi dei componenti principali (PCA) dalla spiegazione al codice python](https://static.wixstatic.com/media/3c029f_c76162f7f3fb4f8c9946aadba6a4a2b7~mv2.png/v1/fill/w_568,h_131,al_c,lg_1,q_85,enc_avif,quality_auto/3c029f_c76162f7f3fb4f8c9946aadba6a4a2b7~mv2.png)
Poiché la [[covarianza]] di una variabile con se stessa è la sua varianza (Cov(a,a)=Var(a)), nella diagonale principale (in alto da sinistra in basso a destra) abbiamo effettivamente le varianze di ciascuna variabile iniziale. E poiché la covarianza è commutativa (Cov(a,b)=Cov(b,a)), le voci della matrice di covarianza sono simmetriche rispetto alla diagonale principale, il che significa che le porzioni triangolari superiore e inferiore sono uguali.

**Cosa ci dicono le covarianze che abbiamo come voci della matrice sulle correlazioni tra le variabili?**
In realtà è il segno della covarianza che conta:
- se positivo allora : le due variabili aumentano o diminuiscono insieme (correlate)    
- se negativo allora: uno aumenta quando l'altro diminuisce (correlato inversamente)
Ora che sappiamo che la matrice di covarianza non è altro che una tabella che riassume le correlazioni tra tutte le possibili coppie di variabili, passiamo al passaggio