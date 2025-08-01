La Data Governance consiste nella pianificazione e nell’esecuzione di ==pratiche volte ad acquisire, controllare, proteggere e trasmettere dati,== oltre ad incrementarne il [[Big Data#Valore]] dei dati stessi e degli asset informativi di una organizzazione, attraverso l’esecuzione delle diverse tipologie di [[Big Data#Analisi]]. Quindi rappresenta l’insieme di tutti quei processi che trasformano i dati elementari in informazioni che portano valore al business di un’azienda, e a tutti coloro che usano i sistemi informativi che li contengono. 
I [[Big Data#Varietà|dati strutturati]] hanno un ciclo di vita ben definito:
	che parte dall’acquisizione 
	procede con una graduale pulizia (cleaning); 
	seguono politiche di discovery volte ad effettuare una prima valutazione. 
	Vengono quindi normalizzati affinché assumano le stesse caratteristiche 
	poi aggregati a seconda delle dimensioni di analisi volute
	per poi finire con una ottimizzazione che faciliti l’accesso agli utenti.
	 
I [[Big Data#Varietà|dati non strutturati]] hanno un ciclo di vita comunque ben definito: 
	si parte dall’acquisizione, 
	a cui segue un passo in funzione della tipologia di dato (Audio Split e Audio Deciphering, Video Frame identification e Image Recognition, Text Correction e Text Tagging). 
	Il passo successivo, nel caso di testo, è quello di indicizzare il testo, estrarre delle entità e fare un’analisi semantica per poi comprendere il significato, e poi eventualmente fare Sentiment Analysis; nel caso di audio e/o video si procede ad inferire i metadati relativi ai contenuti.
	
## Data governance principles

Obiettivo della Data Governance è quello di fornire ==valore== ad una organizzazione attraverso il processamento dei dati con una certa velocità, pur sempre mantenendo alta la qualità con l’utilizzo di strumenti pratici, oltre a considerare la sicurezza. Tutte le politiche e i processi devono considerare la dimensione del valore che si vuole portare alle organizzazioni, oltre alla costo/efficacia delle procedure e alla praticità dei sistemi informativi, che hanno un impatto sui costi. 
Di seguito solo elencati e dettagliati quelli che sono i principi della Data Governance. 
### data retention 
L’informazione deve essere mantenuta quanto fisicamente possibile, con i vincoli dati dalle leggi governative, dalle etiche delle aziende e dalla privacy. D’altra parte è importante considerare che l’informazione ha un suo ciclo di vita ([[Big Data#data life-cycle]]) e il suo valore ([[Big Data#Valore]])decade nel tempo, quindi si deve mantenere ==l’informazione su storage il cui costo è relazionato al valore del dato.==
### data quality
I decisori devono poter accedere ai dati ed essere in grado di comprendere il timing con cui questi arrivano, le procedure di riconciliazione dei dati, la completezza e l’accuratezza con cui sono forniti. La qualità del processo di trasformazione dei dati deve essere definita ad ogni passo, dall’acquisizione fino alla trasmissione; devono essere robusti anche gli algoritmi usati per la valutazione della qualità.
### data access
Qualsiasi persona all’interno dell’azienda deve poter accedere alle informazioni, a patto che non vi siano specifiche ragioni legali, commerciali o etiche per cui non devono essere disponibili ad un individuo. Oramai le informazioni sono disseminate all’interno di una organizzazione, motivo che ne fa crescere il valore; quindi sono necessarie alcune ==limitazioni all’accesso.==
### data custody
Ogni ==data item deve essere gestito== da una singola persona ==con un ruolo specifico==. Deve essere creata una matrice di responsabilità in modo da garantire che potenziali problemi siano riconducibili ad uno specifico individuo: da un lato vi è la dimensione tecnica (data stuart responsabile dei processi dei dati), dall’altra vi è la dimensione di business (data owner), responsabile del dato pubblicato verso gli utenti finali.
### data compliance
In qualsiasi sistema informativo i ==dati contenuti sono soggetti a regole da parte di governi ==locali, regionali, nazionali o internazionali; questi vincoli devono essere messi in pratica nelle politiche di Data Governance. Nel processo quindi deve essere garantita la conoscenza aggiornata di tutte le leggi dell’ambito applicativo di pertinenza, e queste devono mettere in pratica.
### data mapping 
La rilevazione e la registrazione di dati che variano velocemente nel tempo attraverso l’intera organizzazione, permette di monitorare e migliorare l’efficacia di business, tenendo conto di quale sia stata la sorgente dei dati, e considerando il mapping interno all’organizzazione che ne ha permesso la pubblicazione.
### data meaning
Tutti gli stakeholders devono poter conoscere il significato dei dati pubblicati e avere una chiara visione di essi: questo è possibile grazie ad una riduzione della ridondanza, dell’ambiguità e dell’inconsistenza, che amplificano la qualità dell’informazione.
### data 3rd -party-control 
Bisogna controllare i dati che vengono scambiati con terze parti che giocano sempre più un ruolo importante, sia perché vengono forniti dati alle aziende esterne, sia perché queste terze parti sono sottoscrittori di dati, o ancora perché si è deciso di dare la delivery dei dati in outsourcing. Si ha quindi la necessità di avere interscambio di dati, quindi è necessario organizzarli per il business. D’ora in avanti per la descrizione degli aspetti della modellazione ci si soffermerà sul meaning e sul
mapping.

## Information systems modelling concepts

Vi sono diverse ==tecniche di modellazione dei dati== che possono essere molto utili nell’ambito della progettazione di soluzioni Big Data. Vediamole nel seguito. 
### Context Diagram (CD) 
Rappresenta in termini generali ==l’interazione del sistema con il mondo esterno: con altri sistemi o con gli utenti che interagiscono con esso==. E’ utile quindi per rappresentare in termini generali come avviene l’interazione con il sistema, oltre a chiarificare le interfacce, e a rappresentarne i limiti.
### Entity Relationship Diagram (ERD) 
E’ una rappresentazione grafica che rappresenta le relazioni tra persone, oggetti, concetti o eventi all’interno del sistema informativo. E’ molto utilizzato per la rappresentazione delle basi di dati, pur avendo il limite di essere molto legato a questi; è una modellazione logica su cui basare quella fisica.
### Data Flow Diagram (DFD) 
==E’ una rappresentazione dei dati e del flusso dei dati attraverso il sistema informativo==, oltre che dei processi di trasformazione dei Big Data. Modella gli aspetti del processo in maniera indipendente dalla tecnologia.

### Dimensional fact modelling (DFM)
La Dimensional Fact Modeling (DFM) è una ==rappresentazione di fatti, misure, dimensioni e gerarchie utilizzate all’interno di un sistema, che permettono agli utenti di accederlo==. A livello concettuale è indipendente dalle tecnologie, e permette facilmente di modellare sistemi analitici anche in ambito Big Data.
è un formalismo grafico ad hoc appositamente ideato per supportare la fase di modellazione concettuale in un progetto di data warehouse. DFM può essere utilizzato anche da analisti e utenti non tecnici.
Il DFM permette di comprendere quindi quali sono i dati disponibili ai fini del consumo dei dati stessi, e come essi possano essere acceduti secondo le varie dimensioni di analisi. Abilita la comprensione dell’informazione, ma non permette di costruire un glossario delle informazioni, quindi un metodo di condivisione più semplice tra tutti coloro che interagiscono con il sistema e che hanno bisogno di dati pubblicati. Il DFM punta su due aspetti chiave della Data Governance:
•meaning, glossario condiviso dagli utenti;
•mapping, consente di avere una visione singola dei dati pubblicati.
#### fatto 
Rappresenta qualcosa di reale e concreto, oggetto di analisi (modella un evento che avviene nella realtà) circa l’ambito di interesse per il processo di analisi dei dati. Ad esempio: vendita, spedizione,assunzione.
#### misure 
Sono attributi numerici continui che esistono all’interno di un fatto, e lo descrivono da diversi punti di vista. Ad esempio: ogni vendita è misurata dai suoi ricavi.
#### dimensione
Sono attributi discreti che determinano la minima granularità adottata per rappresentare i fatti. Ad esempio tipiche per la vendita sono il prodotto, il negozio e la data.
#### gerarchia 
Sono dimensioni discrete legate da relazioni uno-a-uno, e determinano come i fatti possano essere aggregati e selezionati, ai fini del processo di analisi. Esistono le gerarchie conformi, che sono comuni a più fatti all’interno dello schema informativo che si stia osservando. Ad esempio: gerarchie di tempo o geografiche.

