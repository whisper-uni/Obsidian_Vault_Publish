Hadoop: una piattaforma scalabile e affidabile per lo storage e l’analisi condivisa, che è Open Source e gira su hardware commodity, quindi è costo-efficace. Se è necessario avere una maggiore capacità di risorse, basterà aggiungerne qualcuna, per rendere più efficace l’intero sistema (<font color="#2DC26B">scalabilità orizzontale</font>). 
Esistono due strumenti principali in Hadoop, sui quali sono installati tutti gli altri strumenti. • 
##### **File system distribuito Hadoop**: ==parte di archiviazione== ([[HDFS]]) 
E' composto dalle seguenti componenti
- NN: gestisce i metadati del file system, controlla e coordina i DN. 
- DN: gestisce i dischi locali, archivia e recupera blocchi di dati su istruzioni NN. 
- SNN: conserva una copia dei metadati da NN per evitare SPOF. 

##### **MapReduce** – ==parte di elaborazione== ([[MapReduce]])
 è un modello di programmazione distribuito, scalabile, tollerante ai guasti e parallelo per l'elaborazione di big data su un cluster di macchine di base a basso costo e inaffidabili. MR consente di scrivere lavori distribuiti e scalabili con poco sforzo MR ha due sottocomponenti:     
- Job Tracker (JT)
	- JT è un demone in esecuzione in un server dedicato nel cluster per gestire le risorse del cluster e i lavori MR. Le responsabilità principali di JT sono: 
		-  gestione e monitoraggio delle risorse (CPU e memoria) nei TT. 
		- predisposizione del piano esecutivo e coordinamento delle fasi.
		- pianificazione della mappatura/riduzione delle attività al TT. 
		- gestione del ciclo di vita dei lavori (dal momento della presentazione fino al completamento). 
		- mantenere la cronologia dei lavori (statistiche a livello di lavoro). 
		- fornire tolleranza agli errori.
		- JT è inoltre in grado di riconoscere il rack durante la pianificazione delle attività di mappatura/ riduzione. Nella maggior parte dei casi, l'elaborazione avviene nei nodi in cui il blocco dati richiesto è fisicamente disponibile per ridurre il traffico di rete. 
- Task Tracker (TT). 
	- TT è un demone che viene eseguito in ogni nodo slave nel cluster Hadoop. 
	 Gestisce le risorse:
		-  locali (CPU e memoria) come uno slot. Uno slot (chiamato anche contenitore) è un pacchetto
		- logico fisso di una porzione di memoria e CPU per eseguire l'attività di mappatura/riduzione


> [!note]+ Quando inizia il job di MapReduce
> Il job [[MapReduce]] può essere avviato solo dopo che tutti i blocchi sono stati caricati correttamente in HDFS. L'utente ha anche il privilegio di specificare la dimensione del blocco, RF durante il caricamento di big data.
> 

> [!question ]- Quando Utilizzare MapReduce?
> La MR è comunemente preferita per le seguenti applicazioni:
>  • Ricerca, ordinamento, raggruppamento. 
>  • Statistiche semplici: conteggio, classifica. 
>  • Statistiche complesse: PCA, covarianza. 
>  • Pre-elaborazione di enormi quantità di dati per applicare algoritmi di apprendimento automatico. 
>  • Classificazione: bayes naïve, foresta casuale, regressione. 
>  • Clustering: k Means, gerarchico, densità, bi-clustering.
>   • Elaborazione del testo, creazione di indici, creazione e analisi di grafici, riconoscimento di modelli, filtraggio collaborativo, analisi del sentiment

###### MAP 
1. I dati vengono suddivisi in vari split (di dimensioni pari ad un blocco HDFS, ovvero 128 Mb), e ciascuno viene inviato su un Data Node di elaborazione diverso;
2. A valle dello split ciascuno di questi dati in input verrà posto a processamento da parte di un map task, che genererà l’output relativo secondo l’approccio key-value. I map task devono partizionare l’output (merge) e mantenerlo nel singolo Data Node. Questi output vengono poi distribuiti (shuffle) su vari Data Node che rifanno la medesima operazione sui sottoinsiemi di dati partizionati che gli sono arrivati in input.  La catena split/map task/output gira su un singolo nodo, garantendo la località del dato, e senza necessità di replica dei dati in output, perché qualora ci fosse necessità di ricostruire l’output per il failure di un nodo, un altro nodo può ottenere facilmente lo split e rigenerarlo da capo; quindi non è necessario replicare i risultati intermedi dell’elaborazione. 
###### REDUCE
1. Gli output dei vari mapping vengono copiati su un singolo Data Node e a questi poi vengono applicati i reduce task, che vanno a calcolare il risultato finale dell’operazione. Questo procedimento è sottoposto a meccanismi di replica dell’HDFS, in modo che in caso di failure di un nodo, sia possibile ripristinare i dati importanti per le elaborazioni; 
2. Se le risorse di un singolo nodo non sono sufficienti a garantire il rispetto di alcune tempistiche di elaborazione delle operazioni di reduce, si può usare una molteplicità di nodi. Il numero di task di reduce non è direttamente correlato alla dimensione dell’input ma è indipendente; è strettamente correlato alle performance che si vogliono ottenere.

![[Pasted image 20250609223003.png|700]]
####  RACK AWARENESS

> [!important]
> per ridurre al minimo il trasferimento di blocchi (***transfer rate***) tra cluster. Lo scheduler MR utilizza anche la distanza per determinare dove è disponibile la replica più vicina per avviare le attività di map/reduce
> Di seguito è riportata la distanza tipica dei server 
> **D = 0 stesso nodo** 
> **D = 2 distanza tra i nodi nello stesso rack** 
> **D = 4 distanza tra i nodi in rack diversi**
> **D = 6 distanza tra i nodi di diversi data center**
> ![[Pasted image 20250610231834.png|400]]




In Hadoop un concetto fondamentale nella gestione dei nodi è la definizione di prossimità dei nodi. In ***un’architettura distribuita*** è importante considerare come elemento chiave la ***larghezza di banda,*** intesa come il **transfer-rate** tra i nodi su cui girano i processi MapReduce. La **larghezza di banda** può rappresentare dunque una **misura di distanza tra i nodi** di elaborazione, ma questa non può essere facilmente misurata, poiché varia in funzione di cosa stanno eseguendo i processi e quali dati stanno prendendo, oltre alla località dei dati stessi. <u>La larghezza di banda diventa sempre più piccola man mano che si passa da processi che girano su uno stesso nodo a nodi che risiedono sullo stesso rack, passando da nodi di rack diversi dello stesso data center, per poi finire a nodi che risiedono su diversi data center</u>. Quindi si può considerare **la topologia come elemento fondante di questa architettura**. ==in Hadoop si è scelto di basare l’architettura su considerazioni topologiche==, quindi su come è costruito il cluster distribuito.

### Step Invocazioni Hadoop
La Figura 2.21 mostra i demoni che controllano i passaggi nella sequenza di esecuzione di MR. NN gestisce il caricamento e la suddivisione dei big data in blocchi di uguali dimensioni. JT si occupa della gestione del ciclo di vita del lavoro e della formazione dell'IS. La funzione da RR a combinatore viene eseguita nella JVM dell'attività di mappatura. I passaggi (rimescolamento, unione, ordinamento, gruppo) sono gestiti dallo stesso framework di esecuzione MR. I passaggi rimanenti vengono eseguiti riducendo l'attività per terminare l'esecuzione del lavoro. Gli utenti possono definire quasi tutte le funzioni nella sequenza di esecuzione, ma solo le funzioni di mappatura, combinazione, partizionamento e riduzione sono abbastanza comunemente Personalizzate

![[Pasted image 20250625235607.png]]
### COMPONENTI MR e HDFS 
- **NN**: gestisce i metadati del file system, controlla e coordina i DN. 
- **DN**: gestisce i dischi locali, archivia e recupera blocchi di dati su istruzioni NN. 
- **SNN**: conserva una copia dei metadati da NN per evitare SPOF. 
- **JT**: prepara il piano di esecuzione, avvia le attività di mappatura/riduzione ed esegue il coordinamento delle fasi. 
- **TT**: gestisce CPU e memoria come slot, esegue attività di mappatura/riduzione
- **Client HDFS**: un demone che riceve la richiesta di caricamento dei dati e interagisce con NN per inserire blocchi di dati. Può essere eseguito in qualsiasi nodo del cluster Hadoop. 
- **Job Client**: un demone che riceve il lavoro MR e interagisce con JT. Può essere eseguito in qualsiasi nodo del cluster Hadoop. 
- Attività di **mappatura**: esegue una funzione di mappa definita dall'utente, che legge i dati da HDFS come coppie chiave/valore e produce un numero arbitrario di coppie chiave- valore intermedie
- Attività di **riduzione**: esegue una funzione di riduzione definita dall'utente, che raccoglie l'output da tutte le attività della mappa, unisce, ordina, raggruppa i valori che appartengono alla stessa chiave e infine produce un numero arbitrario di coppie chiave-valore.


### YARN
Lo YARN raggruppa le risorse del cluster e le condivide tra strumenti e framework. YARN è essenzialmente un sistema software per la gestione di diversi framework distribuiti. Gestisce e condivide le risorse del cluster in modo granulare (condividendo le risorse in qualsiasi proporzione in base alla sua disponibilità) tra diversi framework distribuiti nello stesso cluster per un migliore utilizzo del cluster. Lo YARN non sa che tipo di applicazione è in esecuzione su di esso. Può essere il lavoro di MR o Spark o Storm. YARN si basa sull'architettura master-slave e ha due componenti principali:

![[Pasted image 20250627003733.png]]
YARN è il Resource Manager di Hadoop. In termini di layer applicativi (si veda la Figura 4) così come HDFS e HBASE sono a livello di Storage, YARN è a livello di Computing, mentre applicativi quali MapReduce o Spark1 utilizzano i servizi messi a disposizione da YARN per permettere ad ulteriori applicazioni di girare su di esse.
![[Pasted image 20250627221925.png|600]]
I componenti di YARN sono: Client Node, Resource Manager, Node Managers e Container. Sui Client Node gira l’Application Client che usufruisce dei servizi Hadoop e YARN permettendo che tutto funzioni gestendo le risorse disponibili. Vediamo nel dettaglio cosa fa ogni componente, vedendo in pratica come funziona una elaborazione YARN. 
1. Un Application Client richiede l’esecuzione di una applicazione YARN al **Resource Manager**.
2. Il Resource Manager a sua volta richiede l’istanziazione di un **Container**, in cui far girare i processi elaborativi, ad un **Node Manager**. 
3. Il **Container** avrà una **Master Application** (essendo la prima ad essere istanziata) che gira in esso. Il processo viene lanciato. 
4. Può succedere che o il processo non ha necessità di ulteriori risorse di quelle disponibili nel Node Manager, oppure può richiedere al Resource Manager di allocare ulteriori risorse, che vengono comunicate dal Resource Manager al Node Manager della Master Application, la quale non farà altro che istanziare ulteriori container su ulteriori nodi, dove gireranno dei processi ulteriori che saranno istanziati volta per volta dai singoli Node Manager.

![[Pasted image 20250627223226.png|600]] 
#### **Resource Manager(RM)**
È un servizio principale e un gestore di risorse centralizzato nel cluster. Indica al node manager di avviare i contenitori per le attività di mappatura/riduzione. **C'è solo un RM nel cluster**. Le funzionalità specifiche di RM sono:
• gestione e condivisione delle risorse del cluster.
• gestire le richieste di risorse.
• fornire sicurezza con Kerberos.
#### **Node Manager**
Ogni nodo slave esegue un demone NM, che gestisce le risorse slave (memoria e CPU). Il NM comunica con RM per registrarsi far parte di un cluster YARN. Le responsabilità di NM sono la creazione, il monitoraggio e l'eliminazione dei Container per l'AppMaster di MR, l'esecuzione dei task di mappatura e riduzione. 
#### **Container**
Il container è un'unità base di allocazione delle risorse in YARN per qualsiasi applicazione/lavoro. Un contenitore è composto  da CPU virtuale e da una porzione di memoria per avviare attività di mappa/riduzione e l'AppMaster di MR. Un container è programmato da RM e supervisionato da NM. In MRv1, gli utenti possono definire il numero di slot di mappatura/riduzione e la sua configurazione in TT. Tuttavia, il grave svantaggio di uno schema basato sugli slot è che i servizi MR dovrebbero essere interrotti per riconfigurare gli slot. Inoltre, gli slot non sono specifici del lavoro. Ad esempio, considera uno slot della mappa configurato con 1 GB di memoria. Anche se un'attività di mappa richiede solo 200 MB, occupa l'intero 1 GB e non rilascerà la memoria inutilizzata fino al completamento o alla conclusione dell'attività. Pertanto, provoca il sottoutilizzo delle risorse. Al contrario, il contenitore in MRv2 è specifico del lavoro. Ad ogni lavoro può essere assegnata una dimensione diversa del contenitore. Ad esempio, il contenitore1 (2 GB di memoria, 1 core logico), il contenitore2 (3 GB di memoria e 2 core logici) possono avere una configurazione diversa. Tuttavia, il numero di contenitori possibili in un NM dipende dal numero di core e dalla dimensione della memoria dedicata a YARN nel particolare NM.

#### Master dell'applicazione MR (MRAppMaster)
Lo YARN fornisce un Application Master per ogni job di MR, Spark, Storm, ecc. Viene creato quando inizia un lavoro MR e distrutto quando termina un lavoro MR. Ogni lavoro MR ha il proprio MRAppMaster dedicato. Se nel cluster sono in esecuzione due lavori MR, verranno eseguiti due MRAppMaster. MRAppMaster gestisce il ciclo di vita del lavoro MR (in MRv1 JT gestisce il ciclo di vita del lavoro). Richiede a RM che i contenitori avviino attività di mappatura/riduzione. La risposta RM contiene informazioni sui container da lanciare. MRAppMaster coordina la mappatura/riduzione delle attività e delle fasi, aggrega registri e contatori dai NM. **Si comporta come un JT di breve durata per ogni lavoro MR. Fornisce tolleranza agli errori per le attività di mappatura/riduzione. MRAppMaster stesso gestisce la maggior parte delle funzionalità MRv1**

#### fasi MapReduce

L’esecuzione di un job MapReduce è seguito da diversi attori: 
- il Client che sottomette il job il Resource Manager che gestisce l’allocazione di risorse 
- i Node Managers che lanciano e controllano i Containers elaborativi
- l’Application Master che fa la coordinazione dell’esecuzione dei vari processi
- l’HDFS che rende possibile la condivisione dei vari job files. 
Vediamo dunque come questi interagiscono tra di loro (si veda la Figura 8). 
1. Il Client si occupa di sottomettere un Job interagendo con il Resource Manager e l’HDFS (Figura 8a)
2. Il Resource Manager inizializza un’Application Master su uno specifico Node Manager, e distribuisce le richieste di split sui nodi dell’HDFS (Figura 8b). 
3. Eventualmente l’Application Master può richiedere l’assegnazione di ulteriori nodi elaborativi (Figura 8c), e quindi consentire l’esecuzione di processi figlio (che possono essere task di Map o di Reduce che interagiscono con l’HDFS) in ulteriori Node Manager (Figura 8c).

![[Pasted image 20250628235126.png]]Quindi sostanzialmente l’esecuzione di un Job di MapReduce si articolare in 4 diverse fasi: 
##### **job submission**
viene invocato il metodo submit() che crea una istanza di JobSubmitter e chiama la classe di submitJobInternal; a questo punto la classe waitForCompletion() verifica lo stato e lo riporta alla console del job sottomesso: se il job è stato completato correttamente vengono visualizzati i job counters, altrimenti viene loggato l’errore verificatosi; 
##### job initialization 
quando la Job Submission richiede al ResourceManager una nuova AppId vengono verificate le specifiche di output, calcolati gli split di input da distribuire sul sistema HDFS, e copiate le risorse necessarie sul file system condiviso; quindi viene istanziato il ResourceManager invocando il metodo submitApplication(); 
##### task assignment 
a questo punto può essere inizializzato il job, il ResourceManager chiama lo schedulatore YARN che alloca un container e lancia l’ApplicationMaster al suo interno su uno specifico NodeManager. L’ApplicationMaster viene inizializzato con gli oggetti che gestiscono il logging dell’esecuzione del job stesso, e a questo punto l’ApplicationMaster identifica dove si trovano tutti gli input split che sono stati calcolati dal Client, e crea un processo Map per ciascuno, in modo tale da rendere possibile al processo Map di leggere il DataSplit corrispondente;
##### task execution
a questo punto avviene la cosiddetta Uberization, ossia la valutazione delle risorse disponibili nel nodo dove risiede l’ApplicationMaster, per verificare che esse siano sufficienti all’esecuzione e al completamento del job. Se ciò non è possibile l’ApplicationMaster richiede i container che gli sono necessari per tutti i Map e i Reduce tasks al ResourceManager; tutti i Map tasks devono essere chiesti prima dei Reduce tasks, e tutte le richieste di Data Locality ( certi mapping e certi reduce possono avvenire specificatamente su certi nodi.) devono essere prese in considerazione dallo schedulatore. L’ApplicationMaster non fa altro che inizializzare un container in ciascun nodo che gli è stato reso disponibile dal ResourceManager. Prima che il task venga eseguito, tutte le risorse necessarie all’esecuzione sono collezionate e ciascun processo figlio viene ad essere eseguito in una JVM dedicata, in modo da evitare che possibili crash del job inficino la corretta esecuzione del NodeManager, al fine di massimizzare l’affidabilità del sistema, che è uno degli scopi principali dell’architettura Hadoop e di MapReduce.

#### Scheduler
Il concetto fondamentale che è alla base di YARN è la gestione ottimale delle risorse disponibili (memoria, CPU e larghezza di banda), anche attraverso una opportuna schedulazione dei processi. Fondamentale è il concetto di ==Locality==, ***intesa come la specifica di dove i container, quindi i processi elaborativi, devono essere eseguiti in termini di quale nodo e quale rack. Quindi è fondamentale avere chiaro quelle che sono le risorse disponibili, oltre alle richieste di localizzazione dei processi che devono essere istanziati. Questi vincoli di località sono importanti per poter utilizzare la larghezza di banda in maniera efficiente,*** oltre al fatto che bisogna considerare che le risorse possono essere chieste dalle applicazioni in maniera dinamica: Upfront quando vengono richieste tutte all’inizio (Spark), o Phased man mano che vi è necessità (MapReduce). Altro aspetto fondamentale riguarda la gestione della schedulazione nel tempo delle varie richieste fatte dalle applicazioni. 
L’obiettivo di qualsiasi allocazione di risorse è quello di gestirle secondo delle policy specifiche. In YARN si utilizza: 
##### First In First Out (FIFO)
viene eseguita per prima la prima richiesta ricevuta, le altre vengono accodate. Ha il beneficio di non avere bisogno di nessuna configurazione, ma pecca nel caso in cui alcune applicazioni richiedano molte risorse per cui altre applicazioni dovranno attendere molto tempo;
> [!example ]- ESEMPIO FIFO
> Nel caso FIFO (si veda la Figura 6a) quando verrà lanciato un Job1 all’istante 0 questo prenderà tutte le risorse disponibili fino al suo completamento. Il Job2 e il Job3 lanciati in seguito devono attendere rispettivamente che i precedenti siano terminati per poter essere lanciati ed eseguiti;
> 
##### Capacity
vengono create delle code dedicate, a ciascuna delle quali viene assegnata una certa capacità di elaborazione e memoria. Le code possono essere ulteriormente suddivise gerarchicamente. Ha il vantaggio di poter variare l’elasticità, quindi le risorse associate a ciascuna coda;
> [!example ]- ESEMPIO CAPACITY
> Nel caso Capacitivo (si veda la Figura 6b) vengono definite due code, QueueA e QueueB: alla QueueA viene assegnato il 75% delle risorse, il restante 25% viene assegnato alla QueueB. Quando viene lanciato il Job1 gli viene assegnata la QueueA, al Job2 viene assegnata la QueueB; il Job3 deve attendere che le risorse di una Queue siano liberate prima di poter essere eseguito.
> 
##### Fair Scheduler
tutte le applicazioni che girano hanno lo stesso share disponibile di risorse. Ha il vantaggio di poter definire code gerarchiche, e ad ognuna può essere attribuita una policy di scheduling di tipo capacitivo o di tipo FIFO.
l Fair Scheduling risulta quindi essere uno dei modi più flessibile per effettuare la schedulazione di risorse, e offre una gestione più evoluta di un cluster condiviso, anche se può sembrare più complicato.
> [!example ]- ESEMPIO FAIR SCHEDULER
> Nel caso Fair (si veda la Figura 6c) vengono comunque definite delle Queue con quantità di risorse definita; a ciascun Job viene dato il giusto share delle risorse. All’inizio al Job1 vengono assegnate tutte le risorse (di entrambe le code, poiché non vi sono altri Job in esecuzione contemporaneamente); quando poi viene lanciato il Job2, a questo li vengono assegnate tutte le risorse della QueueB, e al Job1 devono essere re-istanziate le risorse della QueueA, perché è necessario che il Job2 giri. Quando viene lanciato il Job3 gli vengono assegnate metà delle risorse della QueueB (quindi vengono re-istanziate le risorse al Job2) e prende l’intera QueueB quando il Job2 finisce, e l’intero sistema di risorse quando termina anche il Job1.
> 

![[Pasted image 20250629010434.png]]
##### Dominant Resource Fairness (DRF)

Altro aspetto molto importante in un ambiente di gestione delle risorse condivise è la possibilità di bilanciare l’utilizzo di molteplici tipologie di risorse. YARN gestisce questo problema cercando di modulare l’utilizzo della risorsa dominante rispetto all’utilizzo complessivo del cluster: questo concetto è definito Dominant Resource Fairness (DRF). Vediamo un esempio concreto considerando la Figura 7.
> [!example]- ESEMPIO
> Si supponga di avere un cluster con 100 CPU e 10TB di memoria RAM. Se vi è una applicazione A che richiede 2 CPU e 300 GB di RAM sta richiedono il 2% di CPU, e il 3% di memoria RAM; quindi questa applicazione sta facendo una richiesta "Dominante in termini di memoria". Una applicazione B che richiede 6 CPU e 100 GB di RAM sta richiedono il 6% di CPU, e l’1% di memoria RAM; quindi questa applicazione sta facendo una richiesta "Dominante in termini di CPU". In termini di risorsa dominante quindi l’applicazione B sta richiedendo 2 volte la risorsa dominante rispetto all’applicazione A (6% rispetto al 3%). Quindi YARN allocherà all’applicazione B metà delle risorse che sta richiedendo (quindi 3 CPU e 50 GB di memoria), per poter modulare in maniera più efficiente ed opportuna le risorse tra le due applicazioni

![[Pasted image 20250629011702.png|500]]