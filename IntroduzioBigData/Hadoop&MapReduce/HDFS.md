HDFS è un ==file system distribuito== progettato per memorizzare file di grandi dimensioni, con modalità di accesso in streaming, e che gira su un cluster di ==commodity hardware==. E’ nato per gestire una modalità di lettura e scrittura di file batch, effettuando operazioni su questo per ottenere una serie di informazioni descrittive dei file di grande volume. 
HDFS gestisce i [[Big Data]]  su un cluster di macchine con modello di accesso ai dati in streaming. Utilizza l'archiviazione distribuita per fornire una visualizzazione del disco singolo e per fornire uno spazio dei nomi globale univoco sull'archiviazione ([[#^nameNode]]) distribuita. 
Si tratta di un file system appositamente progettato con funzionalità quali:
	==distribuzione==
	==tolleranza agli errori==
	==replica== 
	==distribuito su macchine a basso costo e inaffidabili==. 
	Dal punto di vista dell'utente, sembra essere un grande spazio di archiviazione centralizzato, ma dal punto di vista del sistema è il singolo server che contribuisce al suo spazio di archiviazione. HDFS fornisce l'astrazione del file, il che significa che un file oltre la dimensione del disco di archiviazione viene partizionato in [[#<font color=" 2DC26B">HDFS Block</font>| HDFS Block]] e archiviato in un cluster di nodi. Per un utente normale, il file enorme viene logicamente mostrato come un singolo file, ma in realtà parti di questo file sono archiviate in diversi nodi nel cluster. HDFS è immutabile, il che significa che è possibile solo il caricamento iniziale, non esiste alcuna funzionalità di modifica dei file in HDFS utilizzando vi, gedit, ecc. poiché comporta un enorme sovraccarico di I/O, non supporta l'operazione di aggiornamento, ==pertanto i dati in HDFS vengono scritti una volta e letti molte volte (WORM)==


> [!success]+ Quando uso l'HDFS?
> Usa HDFS quando vuoi
• archiviare dati di grandi dimensioni (oltre TB) su server di base. 
• elaborare un numero limitato di file grandi rispetto a un numero elevato di file piccoli files. 
• letture batch invece di letture/scritture casuali. 

> [!failure]+  Quando non uso l'HDFS
Non utilizzare HDFS 
• per il processo di transazione e accesso a bassa latenza (in ms). 
• elaborare molti file di piccole dimensioni (HDFS richiede più metadati e risorse). 
• per la scrittura parallela (HDFS supporta il WORM). 
• alla lettura randomica (HDFS fornisce solo la lettura batch).  ^491498


HDFS ha tre sottocomponenti: 
	one ore more Name Nodes (masters) 
	a set of data nodes (workers) Name nodes maintain the filesystem namespace Datanodes store and retrieve blocks

```mermaid
flowchart LR
A[HDFS] --> B(Name Node) 
A --> D(Secondary Name Node) 
A --> C(Data Node)
B-->E(HDFS Block)
C--> E
E-->F(128 MB)
````


1. <font color="#2DC26B"><font color="#2DC26B">Name Node</font> (NN)</font> : NN è un servizio/daemon centralizzato che funge da gestore di archiviazione del cluster. ^NameNode
	Le sue responsabilità principali sono: 
		• mantenimento dei metadati di file e directory,  il namespace del filesystem e tutti i metadati accessori che lo definiscono (ultima modifica, ultimo accesso, privilegi)
		• controllo e coordinamento dei DN per le operazioni del sistema file come creare, leggere, scrivere, ecc. I client comunicano con NN per eseguire le operazioni quotidiane. A sua volta, NN fornisce ai client la posizione dei DN nel cluster (dove è disponibile il blocco dati) per eseguire operazioni. 
2. <font color="#2DC26B">Secondary Name Node</font> (SNN) : è La replica dei Name Node garantisce una prevenzione alla perdita dei dati, quindi alta affidabilità, pur essendo comunque Single Point of Failure (SPoF). Hadoop ha introdotto il concetto di active/stand-by: in caso di failure del Name Node attivo, un Name Node precedentemente  (SNN)mpassivo viene attivato per gestire il tutto, spostando i dati nell’area di memoria del Name Node che era passivo. Questo però non garantisce l’assenza di perdita dei dati, poiché non vi è una replica costante.
3. <font color="#2DC26B">Data Node (DN)</font> : Il demone DN è responsabile della gestione dei dischi di archiviazione locali. Gestisce le operazioni del file system come la creazione, la lettura, l'apertura, la chiusura e l'eliminazione dei blocchi.
	Il DN non sa nulla dei blocchi dati. **Memorizza ogni blocco come file nel file system locale**. I blocchi vengono caricati/eliminati nei DN in base alle istruzioni di NN, che convalida ed elabora le richieste dei client. **NN non esegue alcuna operazione di lettura/scrittura per i client. I clienti comunicano con NN per conoscere la posizione dei blocchi e reindirizzati ai DN per eseguire operazioni di lettura/scrittura. ^cb740c
	
 Ogni ==blocco== può essere in ==cache ad un solo Data Node==, cosicché il ==Name Node sappia in quale Data Node è cachato il blocco, quindi darà un accesso privilegiato alle operazioni dei Map su quello specifico nodo.
#### <font color="#2DC26B">HDFS Block</font>

**L'unità di archiviazione e accesso ai dati in HDFS è un ==blocco==, che denota la ==quantità minima== di dati che possono essere archiviati e recuperati da HDFS.** I ==dati che volevamo caricare su HDFS vengono divisi in blocchi di uguali dimensioni e archiviati nei DN nel cluster==. **I DN memorizzano ciascun blocco di dati come file nel relativo file system locale**. Il file system Linux utilizza una dimensione di blocco logico di 4 KB (un gruppo di più blocchi fisici) . I blocchi piccoli sono adatti per i database transazionali.. FS di Linux mantiene i metadati a livello file. HDFS utilizza la ==dimensione del blocco logico di 128 MB==. **Pertanto, mantiene i metadati a livello di blocco semplificando la gestione di tali blocchi da parte del Name Node**. HDFS è un file system logico sopra file system locale. Non è un vero e proprio sistema file come ext3, ext4 che funziona a livello di disco fisico. Pertanto, HDFS viene eseguito su sistemi file locali (ext3/ext4) e non interagisce direttamente con i dispositivi di archiviazione

#### Using Filesystem APIs

Il file system è una classe astratta che rappresenta un generico file system, il cui accesso è governato da Application Programming Interface (API). Per creare una istanza di un generico file system, si chiama il metodo **FileSystem.get()**; quindi la classe **HdfsWrite** chiama il metodo **create()** per creare un file su HDFS. Per leggere i dati da un file, si usa la classe **HdfsReader**, che chiama il metodo **open()** per aprire un file in HDFS, che ritorna un InputStream che può essere utilizzato per leggere i contenuti di un file. Per creare delle directory, il file system fornisce il metodo mkdirs(Path f), dato un certo path (f); se il path non esiste viene creato. Su un file system possono essere fatte qualsiasi operazioni, come ad esempio listStatus (per avere una lista di file), getFileStatus (per avere informazioni sul file), globalStatus (per gestire file patterns), e delete (per cancellare).

> [!example]- Esempio : Read file from the local file system and write it to HDFS
> Configuration conf = getConf();
>  OutputStream os = fs.create(outputPath); 
>  InputStream is = new BufferedInputStream(new FileInputStream(localInputPath));
>   IOUtils.copyBytes(is, os, conf);
> 

### Lettura di un File

Vediamo come avviene un’operazione di lettura di un file, e come viene distribuita tra Data Node e Name Node. 
Per la lettura di un file:
- si apre una connessione al DistributedFileSystem, il quale legge dal Name Node le invocazioni dei blocchi, che vengono restituiti ordinati rispetto alla facilità di accesso ai nodi che contengono i file, dando priorità ai Data Node che sono sullo stesso rack, piuttosto che a quelli presenti sullo stesso nodo in cui gira il client; ([[Hadoop#RACK AWARENESS]])
- si leggono i vari Data Node per poi, alla fine, chiudere la connessione con il file system tramite la funzione FSDataInputStream.
![[Pasted image 20250610221938.png|500]]

Passaggio 1: l'utente avvia un comando di lettura al client HDFS, che inoltra la richiesta a NN per trovare la posizione dei blocchi per il file richiesto. 
Passaggio 2: NN fa riferimento ai suoi metadati e trova un elenco di DN in cui è stato archiviato ciascun blocco. Questo elenco viene preparato in base alla posizione (riconoscimento nel rack) delle copie in blocco.
Passaggio 3: il client HDFS è pronto per leggere blocchi da diversi DN creando un flusso di input HDFS.
Passaggio 4: i**l client HDFS preferisce i DN vicini al client (per ridurre il traffico di rete). Se il primo DN dell'elenco non è raggiungibile, viene scelto il secondo DN dell'elenco.**
Passo 5: I blocchi di un file vengono letti in sequenza uno per uno secondo l'ordine di costruzione del file originale. Non è utile leggere più blocchi contemporaneamente. Infine, i DN trasmettono i blocchi di dati al client in ordine

### Scrittura di un file

  Un HDFS Client che gira su un Client Node crea una istanza della classe DistributedFileSystem (1), la quale a sua volta tramite una Remote Procedure Call (RPC) (2) crea (Create) in un NameNode una istanza del file. Il NameNode a questo punto verifica che il Client abbia tutti i privilegi necessari per scrivere quel file nella posizione in cui è richiesto. Quando questo è verificato, se possibile (altrimenti viene generata un Exception), 
   l’HDFS Client crea una istanza della classe FSDataOutputStream e a questo punto può esser cominciata la scrittura (3) vera e propria. 
   La classe FSDataOutputStream splitta la scrittura (4) in tanti pacchetti di dati, che vengono distribuiti iniziando dal DataNode identificato dal NameNode, e man mano che i pacchetti vengono scritti sono generate delle repliche su ulteriori DataNode. Oltre questo viene generata una coda di Acknowledge (5) per la verifica dell’effettiva scrittura del pacchetto. 
   Una volta che il file viene ad essere chiuso l’HDFS Client manda una richiesta di chiusura (6) al FSDataOutputStream: questo rilegge la coda di Acknowledge per verificare che sia completata, e permette la chiusura del file avvisando anche il NameNode, che avrà chiaro tutta la disposizione del file sui vari DataNode.

![[Pasted image 20250610234547.png|500]]


Passaggio 1: una volta che il client HDFS riceve la richiesta di caricamento del file, divide fisicamente il file in blocchi  [[HDFS#<font color=" 2DC26B">HDFS Block</font>|Blocco]] e richiede NN dove archiviare tutti questi blocchi.Poiché il client HDFS non sa quale DN dispone di spazio libero e dove archiviarlo in base al riconoscimento del rack([[Hadoop#RACK AWARENESS]]). 
Passaggio 2: NN si riferisce ai metadati (file FSImage) e determina tre posizioni in base alla consapevolezza del rack per ciascun blocco. Quindi, NN invia un elenco di tre posizioni DN per ciascun blocco. Supponiamo che le posizioni per il blocco 1 siano DN1, DN2 e DN3. Il suggerimento del numero di DN dipende dalla RF. Per impostazione predefinita, vengono suggeriti tre DN per ciascun blocco poiché RF predefinito è 3. Se il nodo client si trova nel cluster Hadoop, è il primo nodo a copiare il blocco dati. 
Passaggio 3: dopo aver ricevuto tre posizioni per ciascun blocco, il client HDFS è pronto per scrivere i blocchi rispettivi DN in parallelo aprendo il flusso di output HDFS. Non vi è alcun vincolo che il blocco 2 debba copiato su HDFS solo dopo il blocco 1. Tutti i blocchi vengono copiati nel cluster in base al numero di thread che un client HDFS può servire.
Passaggio 4: il client HDFS divide ulteriormente logicamente il blocco 1 in una coda di pacchetti (ciascuno da 64 KB), denominata coda dati. Per block1, il client HDFS forma una pipeline con DN1, DN2 e DN3. 
Passaggio 5: il primo pacchetto dalla coda dati viene copiato su DN1, che memorizza e inoltra il pacchetto a DN2 lungo la pipeline. 
Passaggio 7: il client HDFS riceve una conferma dai DN che indica che il blocco è stato copiato correttamente. Il client HDFS invia un messaggio di successo all'utente. Tutti questi processi sono altamente trasparenti per l'utente. L'utente non sa dove sono archiviati i blocchi di dati. 



