Una **tabella hash** (o in inglese _hash table_) è una struttura dati utilizzata per archiviare e recuperare dati in modo molto efficiente. Funziona mappando le chiavi a valori, in modo simile a un dizionario, ma con un meccanismo interno che la rende estremamente veloce per le operazioni di ricerca, inserimento e cancellazione.

L'idea fondamentale di una tabella hash è quella di utilizzare una [[Funzione hash]] per calcolare una posizione (un "indice" o "indirizzo") all'interno di un array (spesso chiamato "array di slot" o "bucket") dove il dato deve essere memorizzato.

### Come funziona una Tabella Hash:

1. **Chiave (Key):** È il dato che vuoi utilizzare per identificare univocamente un valore. Ad esempio, in una rubrica, il nome di una persona potrebbe essere la chiave.
2. **Valore (Value):** È il dato che vuoi archiviare, associato a una chiave. Ad esempio, il numero di telefono di quella persona.
3. [[Funzione Hash]]: È un algoritmo matematico che prende la chiave in input e restituisce un numero intero (l'indice) che corrisponde a una posizione nell'array. L'obiettivo della funzione hash è quello di distribuire le chiavi in modo uniforme il più possibile nell'array per minimizzare le collisioni.
4. **Array (o Tabella):** È l'area di memoria dove i dati vengono effettivamente memorizzati, in base agli indici calcolati dalla funzione hash.

**Processo di Inserimento:**
- Prendi la chiave del dato da inserire.
- Applica la funzione hash alla chiave per ottenere un indice numerico.
- Memorizza il valore associato alla chiave nella posizione dell'adicata da quell'indice.
**Processo di Ricerca:**
- Prendi la chiave del dato che vuoi cercare.
- Applica la stessa funzione hash alla chiave per ottenere l'indice.
- Vai alla posizione nell'array indicata da quell'indice e recupera il valore.
### Vantaggi delle Tabelle Hash:
- **Velocità:** In media, le operazioni di ricerca, inserimento e cancellazione hanno una complessità temporale di **O(1)** (tempo costante). Questo significa che il tempo necessario per queste operazioni rimane praticamente lo stesso indipendentemente dalla quantità di dati, purché la tabella sia ben progettata e le collisioni siano gestite efficacemente.
- **Efficienza:** Sono molto efficienti per i casi d'uso in cui è necessario accedere rapidamente ai dati tramite una chiave.
### Svantaggi e Problemi:
- **Collisioni:** È il problema principale. Due chiavi diverse possono produrre lo stesso indice tramite la funzione hash. Quando questo accade, si verifica una **collisione**. Le collisioni devono essere gestite per evitare la perdita di dati o l'errata lettura.
    - **Gestione delle Collisioni:** Le tecniche più comuni includono:
        - **Concatenamento (Chaining):** Ogni slot dell'array non contiene un singolo dato, ma una lista (o un'altra struttura dati) di tutti i dati che hanno lo stesso hash.
        - **Indirizzamento Aperto (Open Addressing):** Se uno slot è già occupato, si cerca sistematicamente un altro slot libero (es. _linear probing_, _quadratic probing_, _double hashing_).
- **Costo della funzione hash:** Una funzione hash mal progettata o troppo complessa può rallentare le operazioni.
- **Fattore di Carico (Load Factor):** È il rapporto tra il numero di elementi memorizzati e la dimensione totale dell'array. Un fattore di carico troppo alto (tabella troppo piena) aumenta la probabilità di collisioni e degrada le prestazioni. Spesso, quando il fattore di carico supera una certa soglia, la tabella viene "ridimensionata" (rehashed), cioè si crea un array più grande e tutti gli elementi vengono ri-inseriti con la funzione hash.
### Applicazioni Comuni:
Le tabelle hash sono onnipresenti nell'informatica e vengono usate in:
- **Database:** Per indicizzare i dati e velocizzare le query.
- **Cache:** Per memorizzare dati a cui si accede frequentemente.
- **Compilatori:** Per tabelle dei simboli.
- **Sistemi operativi:** Per gestire le tabelle dei processi o dei file.
- **Linguaggi di programmazione:** Molti linguaggi (come Python con i suoi dizionari, Java con le HashMap, JavaScript con gli oggetti) implementano strutture dati basate sulle tabelle hash.
- **Crittografia:** Le funzioni hash crittografiche sono un tipo specifico di funzione hash utilizzata per garantire l'integrità dei dati e per la sicurezza.
In sintesi, una tabella hash è uno strumento potentissimo per l'archiviazione e il recupero efficiente dei dati, purché le collisioni siano gestite in modo appropriato e la funzione hash sia ben scelta.