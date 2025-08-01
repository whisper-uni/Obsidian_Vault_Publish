![[MappaBigData.png]]
Il Big Data è definito come:
**Estrazione "conosciuta" da un immenso volume, varietà e velocità dei dati, nel contesto in cui si trovano, oltre ciò che
era precedentemente possibile.**
Ci si riferisce ad una estrazione "intuitiva" di informazioni che possono apportare un certo valore. Tutto questo deriva da una necessità di governare la cosiddetta "Digital Density", cioè il valore che i dati portano all’economia, attraverso l’integrazione delle interazioni tra i singoli Data Points, oltre alla alla necessità di governare questa moltitudine di informazioni.
Caratteristiche fondamentali dei Big Data sono le cosiddette "5 + 1 V" dei Big Data: 
### Volume
Le organizzazioni devono gestire più dati in diverse forme attraverso un ampio numero di sistemi, considerando che il costo dello storage (per costo di realizzazione) è in diminuzione, al contrario del processing power1
### Varietà
 I dati non sono omogenei, bensì molto eterogenei: il ==20% è dato strutturato==, l’==80% non strutturato==
### Velocità
 Indica il rate a cui i dati sono generati e consumati, o l’abilità di fare streaming e/o processare le informazioni che fluiscono a velocità rapida, spessissimo in real time.
### Veridicita
È necessario conoscere la provenienza del dato e l’integrità, tenere traccia della storia di eventuali cambiamenti apportati ai dati (la cosiddetta retention) quanto tempo vanno mantenuti i dati e con quali modalità, e fare una analisi approfondita circa la rilevanza di essi in alcune attività.
### Vulnerabilità
I dati devono essere protetti e la sicurezza deve essere considerata durante la progettazione dei sistemi; importante è la sicurezza multi-livello.
### Valore 
Le organizzazioni che orientano il loro Business su attività di Data Driven, e che quindi adottano sistemi per l’acquisizione, l’analisi e la gestione dei dati, sono nella media il 5% più profittevoli dei loro competitors, riuscendo a portare valore a loro stesse e nell’ambito in cui si trovano.
### data life-cycle
Aspetto fondamentale è legato al [[#Valore]] del dato che diminuisce nel tempo. Si parla di "dimezzamento" del dato: il rate a cui questi dati decadono è diverso a seconda dell’ambito; stessa discorso vale per i fattori che impattano questo decadimento, diversi a seconda della categoria (detta data item). In un diagramma in cui sull’asse delle ascisse poniamo l’half-life dei dati, se questo è basso il rate di decadimento del valore del dato è veloce (è il caso di retail, internet, turismo), se è alto il rate di decadimento è più basso (healthcare,chemistry, industry, agricoltura).

## Analisi
 il tipo di relazione che si ha con la catena di valore del dato stesso.
 Il [[#Valore]] che otteniamo a fronte dell’utilizzo dei dati ==è tanto più alto passando da un’analisi descrittiva verso una prescrittiva.==
La distinzione tra le diverse tipologie di analisi:
###  Descrittive
L'**analisi descrittiva** è il livello più basilare e risponde alla domanda =="Cosa è successo?"==. Si concentra sulla **sintesi e sulla rappresentazione dei dati storici** per capire le caratteristiche di base di un fenomeno. È come scattare una fotografia di ciò che è accaduto.
**Caratteristiche principali:**
- **Riepiloga i dati passati:** Utilizza statistiche come media, mediana, moda, deviazione standard per descrivere i trend e le distribuzioni.
- **Visualizzazione:** Spesso presenta i dati tramite grafici, tabelle e dashboard per renderli facilmente comprensibili.
- **Obiettivo:** Fornire una chiara panoramica di eventi passati, identificare modelli e anomalie.
- **Esempi:**
    - Un'azienda che analizza le vendite del trimestre precedente per capire quali prodotti hanno venduto di più.
    - Un'analisi del traffico di un sito web per vedere quante visite ha ricevuto e da quali fonti.
    - Il calcolo del numero di clienti persi nell'ultimo anno.
Semplici analisi che permettono di condensare tutti i Big Data in informazioni più piccole e gestibili. Con questa tipologia di analisi è nata la Business Intelligence (BI), il Data Warehouse e il Reporting. Lo scopo è quello di "sommarizzare" ciò che è avvenuto attraverso i dati. Più dell’80% delle Business Analytics - includendo [[Social Analitycs]] - sono descrittive.
### Predittive
L'**analisi predittiva** va oltre il semplice racconto del passato e cerca di rispondere alla domanda =="Cosa potrebbe succedere?"==. Utilizza dati storici, modelli statistici e algoritmi di machine learning per **prevedere eventi futuri o risultati probabili**.
**Caratteristiche principali:**
- **Previsione:** Sviluppa modelli che imparano dai dati passati per fare previsioni su eventi futuri.
- **Probabilità:** Non fornisce certezze assolute, ma stime di probabilità su ciò che potrebbe accadere.
- ==**Tecniche:** Si avvale di tecniche come regressione, alberi decisionali, reti neurali e altri algoritmi di machine learning.==
- **Obiettivo:** Anticipare le tendenze, identificare i rischi e le opportunità future.
- **Esempi:**
    - Un'azienda di e-commerce che predice quali prodotti un cliente potrebbe acquistare in base alla sua cronologia di acquisti.
    - Previsione della domanda di un prodotto per ottimizzare la gestione delle scorte.
    - Valutazione del rischio di insolvenza di un cliente basata sul suo storico finanziario.
    - Previsione del fallimento di un componente meccanico per la manutenzione preventiva.
Queste analisi utilizzano una serie di statistiche, tecniche di modellazione, Data Mining e [[Machine Learning]] per valutare dati storici e recenti, da fornire in input ai sistemi, al fine di effettuare valutazioni in termini probabilistici di quello che il modello genera come output.
### Prescrittive
L'**analisi prescrittiva** è il livello più avanzato e sofisticato, e risponde alla domanda =="Cosa dovremmo fare?".== Non solo prevede cosa potrebbe accadere, ma **suggerisce le migliori azioni da intraprendere** per ottenere un risultato desiderato o evitare un esito negativo. Va oltre la previsione, fornendo raccomandazioni concrete e attuabili.
**Caratteristiche principali:**
- **Raccomandazioni:** Fornisce opzioni e suggerimenti su come agire per influenzare i risultati.
- ==**Ottimizzazione:** Spesso utilizza tecniche di ottimizzazione, simulazione e machine learning per trovare la soluzione migliore considerando vari vincoli e obiettivi.==
- **Decisione:** Aiuta a automatizzare e migliorare il processo decisionale, rendendolo più basato sui dati.
- **Obiettivo:** Ottimizzare i risultati, mitigare i rischi e guidare le azioni per raggiungere obiettivi specifici.
- **Esempi:**
    - Un sistema che suggerisce il percorso di consegna più efficiente per una flotta di veicoli, considerando traffico, tempo e costi.
    - Un'azienda che consiglia strategie di prezzo dinamiche per massimizzare i ricavi in base alle previsioni di domanda.
    - Sistemi sanitari che raccomandano piani di trattamento personalizzati per i pazienti, basandosi sulle previsioni di efficacia e sui profili dei pazienti.
    - Un sistema di gestione del portafoglio finanziario che suggerisce quali investimenti fare per massimizzare i profitti e minimizzare i rischi.
Tali tecniche vengono adottate qualora sia necessario "prescrivere" un’azione, così che il Decision Maker possa prendere le informazioni risultanti e agire di conseguenza. Utilizzano algoritmi che valutano probabilisticamente quale sia la migliore azione da intraprendere per arrivare ad un certo obiettivo, o raccomandano più possibili azioni, mostrando l’outcome più probabile per ogni decisione. L’idea è quella di generare una raccomandazione rispetto a quella che può essere la migliore ed efficace azione da intraprendere. 

### Sintesi
l'**analisi descrittiva** ci dice cosa è successo, l'**analisi predittiva** ci dice cosa _potrebbe_ succedere, e l'**analisi prescrittiva** ci dice cosa _dovremmo fare_ per influenzare attivamente il futuro. Nel contesto dei Big Data, queste tre tipologie di analisi sono fondamentali per trasformare grandi volumi di dati in **decisioni strategiche e vantaggi competitivi**.