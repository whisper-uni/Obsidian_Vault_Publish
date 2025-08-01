
![[PCA_mappa.png]]

Una delle diverse tipologie di [[ML Non Supervisionato]] è la Principal Components Analysis (PCA). ==La PCA ha l’obiettivo di derivare, dato un insieme di variabili p su un certo numero n di osservazioni, un set di features con dimensione minore==. Quindi date n osservazioni in uno spazio p  dimensioni siano interessanti tutte allo stesso modo. Questo può succedere perché ==ci sono delle variabili che dipendono dalle altre, e possono essere ottenute come combinazione di un sottoinsieme di variabili==. Dunque si cerca il ==set minimo di variabili che descrivono ugualmente bene, o nei limiti di una certa ==[[Varianza]], l’intero set n di osservazioni date. La PCA vuole fare una valutazione alquanto ==geometrica: ridurre la dimensione di una data matrice nxp identificando le direzioni delle features nello spazio p dimensionale attraverso cui i dati originali (quindi le n osservazioni) siano altamente variabili(con la più alta [[Varianza]]==) .


![[Immagine PCA.png]]

La prima componente principale altro non è che la combinazione lineare normalizzata delle features, quindi delle p colonne della matrice X che ha la più ampia varianza

Le p nuove variabili sono dette componenti principali (o principal components). 
➢ Caratteristiche delle componenti principali: 
	▪ Le **componenti principali sono nuove variabili**, create artificialmente, nessuna di loro coincide con alcuna delle m variabili di partenza. 
	▪ Ogni componente principale è una **combinazione lineare delle m variabili originali.** 
	▪ Le **componenti principali sono tali da riassumere quanta più informazione possibile sulle m variabili originali. **
	▪ Le componenti principali sono ordinate in base a quanta informazione del dataset originale racchiudono (𝑃𝐶1 è la componente più informativa, 𝑃𝐶2 la seconda più informativa ecc.) 
	▪ Le componenti principali per costruzione sono tra loro scorrelate.**
	In pratica la PCA effettua una proiezione ortogonale dei dati su uno spazio definito da nuove dimensioni dette componenti principali. Queste sono tali per cui la varianza delle coordinate dei dati proiettati sulle nuove dimensioni è massima per le prime dimensioni.
	![[Pasted image 20250527235031.png]]

### Perchè utilizzare la PCA?
Visualizzazione
 Quando abbiamo dataset con tante variabili (m grande) diventa difficile rappresentare graficamente i dati per analizzarli dal punto di vista visivo. 
	 ▪ Tipicamente si visualizzano le distribuzioni delle singole variabili o al più gli scatterplot di coppie di variabili. 
	 ▪ Problemi: 
		 • Lo scatterplot di due variabili rappresenta solo una piccola quantità dell’informazione contenuta nei dati. 
		 • Con m variabili dovremmo fare 𝑚 ∙ (𝑚 − 1)/2 scatterplot. Se m = 10 → 10 x 9/2 = 45 scatterplot!
	➢ Possiamo sfruttare la PCA per riassumere l’informazione contenuta nei dati usando poche variabili, più semplici da rappresentare. 
		▪ Potremmo realizzare lo scatterplot delle prime 2 componenti principali, 𝑃𝐶1 e 𝑃𝐶2, ovvero quelle più informative
Compressione Dati
	➢ Compressione: al posto di archiviare le m variabili di partenza, archivio le p componenti principali, con un risparmio in memoria.	
	➢ Decompressione: utilizzando le p componenti principali ricostruisco le m variabili di partenza. La ricostruzione non sarà perfetta, l’errore introdotto dalla compressione dipende da quanto informative erano le p componenti principali selezionate

### PCA, COME SI REALIZZA?

➢ Dataset originale: m variabili, 𝑋1, 𝑋2, … , 𝑋𝑚, a media nulla. 
➢ Nota: se le variabili non sono a media nulla, prima di realizzare la PCA, i dati vanno centrati → ad ogni variabile va sottratta la sua media. 

![[Pasted image 20250527234308.png]]

➢ Trasformazione lineare normalizzata delle m variabili → m nuove variabili, 𝑃𝐶1, 𝑃𝐶2, …,𝑃𝐶𝑚, dette componenti principali tra loro scorrelate 
	𝑃𝐶1 = 𝑣11 𝑋1 + 𝑣21 𝑋2 + … + 𝑣𝑚1 𝑋𝑚 
	𝑃𝐶2 = 𝑣12 𝑋1 + 𝑣22 𝑋2 + … + 𝑣𝑚2 𝑋𝑚 
	𝑃𝐶𝑚 = 𝑣1𝑚 𝑋1 + 𝑣2𝑚 𝑋2 + … + 𝑣𝑚𝑚 𝑋𝑚 
➢ I coefficienti 𝑣𝑖𝑘 si dicono loadings consentono di trasformare le variabili di partenza nelle nuove variabili, le componenti principali.
 I loadings devono essere tali che le prime componenti principali riassumano quanta più varianza possibile delle variabili di partenza: 
 𝑣𝑎𝑟 𝑃𝐶1 > 𝑣𝑎𝑟 𝑃𝐶2 > 𝑣𝑎𝑟 𝑃𝐶3 > ⋯ > 𝑣𝑎𝑟 𝑃𝐶𝑚 
 ▪ 𝑃𝐶1  da sola deve essere in grado di spiegare quanta più varianza possibile dei dati di partenza. 
 ▪ 𝑃𝐶2 da sola deve essere in grado di spiegare quanta più varianza possibile della porzione di varianza non spiegata da 𝑃𝐶1. 
 ▪ … 
 ➢ Considerando solo le prime p componenti principali possiamo efficacemente ridurre la dimensionalità dei dati → nuovo set di p<m variabili che riassume la maggior parte della [[Varianza]] delle m variabili di partenza. 

 Per passare dalle coordinate dei punti nello spazio originale a quelle nello spazio definito dalle componenti principali, basta applicare la trasformazione lineare definita dai loadings

![[Pasted image 20250527233816.png]]

   𝒀  = 𝑿 ∙ 𝑽 
 ➢ ==La matrice V è di fatto una matrice di rotazione che consente di passare dalle coordinate nel sistema di riferimento originale, alle coordinate nel sistema di riferimento delle componenti principali.==

 La PCA ci fornisce dunque una nuova rappresentazione dei dati nello spazio delle componenti principali, 𝑃𝐶1, 𝑃𝐶2, …,𝑃𝐶𝑚, che ha 2 caratteristiche fondamentali: 
 ▪ Le componenti principali sono scorrelate 
 ▪ La varianza dei dati proiettati lungo le componenti principali decresce all’aumentare delle componenti, la maggior parte della varianza complessiva è concentrata nelle prime componenti principali 𝑣𝑎𝑟 𝑃𝐶1 > 𝑣𝑎𝑟 𝑃𝐶2 > 𝑣𝑎𝑟 𝑃𝐶3 > ⋯ > 𝑣𝑎𝑟 𝑃𝐶𝑚 
 ➢ Per ridurre la dimensionalità possiamo considerare solo le prime p componenti principali

COME SI CALCOLANO I LOADINGS?

 Come possiamo calcolare i valori dei loadings, ovvero la matrice V, che mi consente di realizzare la PCA? 
 ➢ Le colonne della matrice V sono gli autovettori della matrice di covarianza di X ordinati secondo l’ordine decrescente dei rispettivi autovalori.
Calcolo della [[matrice di covarianza]] di X: S
➢ Calcoliamo autovalori e autovettori di S.
	Sia 𝑨 ∈ ℝ 𝑁×𝑁 una matrice quadrata di 𝑁 righe e 𝑁 colonne. Se esistono un vettore 𝒗 ∈ ℝ𝑁 e uno scalare 𝜆 (anche complesso) tali che: 
	𝑨𝒗 = 𝜆𝒗 si dice che 𝒗 è autovettore di 𝑨 e 𝜆 il suo autovalore corrispondente. 
	Proprietà: 
	➢ Una matrice di dimensione N x N ha al massimo N autovalori distinti. 
	➢ Gli autovalori sono gli zeri del polinomio caratteristico: 
	det (𝑨 − 𝜆𝑰 )= 0
	
Gli autovettori di S ([[matrice di covarianza]]) rappresentano i loadings che definiscono le componenti principali. 
➢ Le componenti principali sono ortogonali tra loro → quindi scorrelate. 
➢ In che ordine vengono considerati gli autovettori per definire le componenti principali? → In base agli autovalori corrispondenti.

➢ Ordiniamo i gli autovalori dal più grande al più piccolo: 
𝜆1 > 𝜆2 > ⋯ > 𝜆𝑚 
 |.        |               |
𝒗𝟏      𝒗𝟐 …       𝒗𝒎 
➢ L’autovettore 𝒗𝟏 corrispondente all’autovalore massimo, 𝜆1, rappresenta il vettore dei loadings della prima componente principale, ovvero la prima colonna di 𝑽. 
➢ Gli autovettori, 𝒗𝟏, 𝒗𝟐, … , 𝒗𝒎, in questo ordine definiscono le colonne di 𝑽: 𝑽=\[𝒗𝟏 𝒗𝟐 … 𝒗𝒎\] 
==Gli autovalori rappresentano la varianza dei dati proiettati lungo le componenti principali==


### PCA - RIASSUNTO

1. Centramento (ad ogni colonna di X si sottrae la sua media) o  [[Standardizazione]] dei dati:
2. Calcolo della [[matrice di covarianza]] di X → S (m x m) 
3. Calcolo di autovettori e autovalori di S costruendo la matrice V dei loadings. 
		▪ Gli autovettori rappresentano i coefficienti per definire le componenti principali. 
		▪ L’ordine delle componenti principali è stabilito dall’ordine degli autovalori. 
		▪ L’autovettore corrispondente all’autovalore massimo rappresenta i coefficienti (loadings) della prima componente principale. 
4. Trasformazione dei dati passando alle coordinate nello spazio delle componenti principali: Y=X·V 
5. Scelta delle prime p componenti principali che rappresentano gran parte della varianza delle variabili originali (scree plot o plot della frazione di varianza spiegata dalle prime p componenti). 
6. Le coordinate delle n osservazioni lungo le p componenti principali rappresentano il dataset trasformato e ridotto. 

### SCELTA DEL NUMERO DI COMPONENTI PRINCIPALI (SCREE PLOT)

![[Pasted image 20250528003511.png]]