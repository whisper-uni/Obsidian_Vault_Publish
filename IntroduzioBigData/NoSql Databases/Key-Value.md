I database Key-Value sono basati sul concetto di Associative Arrays(è un array i cui elementi sono accessibili mediante stringhe anziché indici puramente numerici), ottenuti tramite l’associazione tra chiave e valore/i. Questi sono un concetto molto più flessibile da un lato e molto più ampio dall’altro dei vettori classici: non sono ristretti come i normali array, e permettono di utilizzare interi come indici o di limitare i valori allo stesso tipo. 
Un database Key-Value altro non è che una [[Tabella hash]] che rappresenta un array associativo, le cui chiavi sono uniche, quindi gli indici sono unici, e possono essere di qualsiasi tipo. 
La chiave viene trasformata in una chiave hash attraverso l’utilizzo di una [[funzione hash]]: 
- si parte dalla stringa che rappresenta la chiave e la si converte in una stringa di interi (valore binari), costituita da un Major Key Components (MKC), 
- e opzionalmente, da uno o più minor key components (mkc). 
Se i mkc sono utilizzati, la combinazione del MKC e del/dei mkc identifica univocamente un singolo record nello store. Questo è fatto in maniera tale che le chiavi vengano ad essere distribuite uniformemente nel database distribuito lungo le partizioni orizzontali attraverso l’utilizzo della MKC, che identifica in quale Shard verrà ad essere memorizzato un dato record. 
Le **Shards** sono una **partizione orizzontale** dei dati nel database. Ogni Shard è gestita da un determinato Database Server ed è identificata da una MKC. Questa è una modalità di partizionamento cosiddetta orizzontale, che è diversa da quella classica dei database relazionali (che è una partizione verticale), in cui i dati sono partizionati su server diversi ma per colonna
Altro concetto importante riguarda i valori e la loro gestione nei database distribuiti NoSQL. I valori non sono altro che arrays di byte che non richiedono strong typing: possono contenere stringhe o insiemi di stringhe con l’attributo che le contraddistingue. 
> [!info]- Schema Avro
> In un caso del genere conviene quindi utilizzare il concetto di Schema Avro (basato sul formato JSON) che permette semplicemente di andare a definire degli schemi all’interno del valore, quindi permettendo ai database Key-Value di tipizzare il contenuto del valore. Tipicamente lo Schema Avro è salvato all’interno di un file che lo descrive. Per poterlo utilizzare si fa un binding: attraverso il comando ddl add-schema (kv -> ddl add-schema -file PersonSchema.avsc) si aggiunge al Key-Value che sto considerando lo Schema Avro in modo tale che possa leggerlo. Per rendere disponibile lo Schema Avro al codice bisogna effettuare un parsing (final Schema.Parser parse = new Schema.Parser();), e andare a leggerlo (perser.parse(new File("PersonSchema.asvc"))), quin- di renderlo disponibile all’applicazione (final Schema PersonSchema = parser.getTypes().get ("FVavro.PersonaInformation")). Questo consentirà di andare a leggere il contenuto dello schema stesso in termini di tipi resi disponibili, quindi sarà possibile aggiungere i campi che contraddistinguono lo schema dell’applicazione, creando un binding, quindi una translation dal valore contenuto nel database Key- Value alle istanze di Schema Avro che si vanno a considerare. Solo a questo punto si hanno a disposizione i contenuti singoli di ciascun campo contenuto all’interno dello Schema Avro definito per quel particolare value associato alla chiave. Questo è valido per qualsiasi operazione si effettui su un database key-value store. Tali operazioni posso essere quindi riassunte nelle seguenti: 1. Retrieve di un valore attraverso una singola chiave; 2. Inserire un valore, o modificarlo, attraverso la chiave; 3. Cancellare il valore attraverso la chiave. In alcuni database key-value si possono utilizzare le versioni da associare al valore per migliorare la consistenza. Quindi in generale, viste le operazioni che è possibile effettuare su un Key-Value database, si possono avere difficoltà quando si vanno ad effettuare operazioni di ricerca.
> 


### key-value architecture


L’architettura di un database Key-Value è costituita da:
- ==Storage Nodes== -->  ciascun Storage Node contiene uno o più Replication Nodes a seconda della sua capacità in termini di storage
	- ==Replication Nodes== --> ogni Replication Node si può pensare come a un singolo database contenente tabelle o coppie chiave-valore suddivise in almeno una partizione:
		- ==Partizione== --> Una **partizione** è un **sottoinsieme dei dati** totali, raggruppato in base a una **chiave hash**. Quindi le chiavi sono inserite in contenitori logici chiamati partizioni 
	 I ==Replication Nodes== sono organizzati in ==Shard== . Un singolo Shard contiene più nodi di replicazione e un nodo master . Il nodo master esegue tutte le attività di scrittura sul database. Ogni ==Shard== contiene anche una o più repliche di sola lettura . Il nodo master copia tutti i nuovi dati delle attività di scrittura sulle repliche. Le repliche vengono quindi utilizzate per gestire le operazioni di sola lettura.
	 In caso di guasto della macchina che ospita il nodo master, il master esegue automaticamente il failover su uno degli altri nodi nello shard. Uno dei nodi replica viene promosso automaticamente a master. Sebbene possa esserci un solo nodo master per shard in un dato momento, qualsiasi altro membro dello shard può diventare un nodo master.
	 Quindi lo Shard è composto da: 
		**Uno Storage Node "Replication Master" (o Leader):** Questo è il nodo principale responsabile delle operazioni di scrittura per e coordina le repliche. 
		**Uno o più Storage Node "di Replica" (o Follower):** Questi sono nodi aggiuntivi che contengono copie identiche (repliche) dei dati del nodo primario. Il loro scopo è garantire la disponibilità dei dati in caso di fallimento del nodo primario e, spesso, possono anche servire le letture.
	    **La porzione logica dei dati o partizioni:** Questa è la parte specifica del dataset totale che questo gruppo di nodi è responsabile di gestire. 

![[Pasted image 20250708004805.png]]

In generale un'architettura tipica utilizzata da un'applicazione che utilizza un database NoSQL . 

![[Pasted image 20250708005328.png]]