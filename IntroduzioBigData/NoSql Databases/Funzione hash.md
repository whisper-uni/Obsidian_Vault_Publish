## Cos'è una Funzione Hash?

Una **funzione hash** è un algoritmo matematico che prende un input (spesso chiamato "chiave" o "messaggio") di dimensione arbitraria e restituisce un output di dimensione fissa, solitamente un numero intero, chiamato **valore hash**, **codice hash**, **digest hash** o semplicemente **hash**. Immagina di avere una macchina che, non importa cosa tu le dia in pasto (una parola, una frase, un intero libro), sputa sempre fuori una stringa di caratteri di una lunghezza predefinita.
## Caratteristiche Fondamentali delle Funzioni Hash
Per essere efficace in una tabella hash o in altre applicazioni, una funzione hash dovrebbe avere alcune proprietà chiave:
###### 1. **Deterministica:**
Per lo stesso input, la funzione deve sempre produrre lo stesso output. Se dai "ciao" alla funzione oggi e ottieni "123", anche domani, dandole "ciao", dovrai ottenere "123".
###### 2. **Veloce da Calcolare:** 
Il calcolo dell'hash deve essere rapido ed efficiente per non rallentare le operazioni della struttura dati.
###### 3.**Distribuzione Uniforme (ideale):** 
L'obiettivo è che la funzione distribuisca gli input in modo più uniforme possibile tra tutti i possibili valori hash. Questo significa che dovrebbe minimizzare le **collisioni**, cioè situazioni in cui due input diversi producono lo stesso valore hash. Se la funzione raggruppa molti input sullo stesso hash, la tabella hash perderà efficienza.
###### 4. **Resistenza alle Collisioni (per funzioni crittografiche):**
Nelle funzioni hash crittografiche (come MD5, SHA-256), questa proprietà è cruciale. Significa che deve essere estremamente difficile trovare due input diversi che producono lo stesso output hash. Questo le rende utili per verificare l'integrità dei dati.

## Tipi di Funzioni Hash e Loro Applicazioni

Esistono vari tipi di funzioni hash, progettate per scopi diversi:

- **Funzioni Hash per Tabelle Hash (Non Crittografiche):**
    - Utilizzate principalmente per le **tabelle hash** per mappare in modo efficiente le chiavi a posizioni di memoria.
    - L'obiettivo principale è la velocità e la buona distribuzione per minimizzare le collisioni.
    - Esempi: Spesso usano operazioni matematiche come bitwise shifts, XOR, moltiplicazioni e divisioni (modulo) per mescolare i bit dell'input e produrre un h
- **Funzioni Hash Crittografiche:**
    - Molto più complesse e robuste.
    - Devono essere **unidirezionali** (impossibile risalire all'input partendo dall'hash) e avere una forte **resistenza alle collisioni**.
    - Utilizzi:
        - **Verifica dell'integrità dei dati:** Se anche un singolo bit di un file cambia, il suo hash cambia completamente. Questo permette di rilevare manomissioni.
        - **Password:** Anziché memorizzare le password in chiaro, i sistemi memorizzano il loro hash. Quando un utente tenta di accedere, la password inserita viene hashata e confrontata con l'hash memorizzato.
        - **Firme digitali:** Per garantire l'autenticità e l'integrità dei documenti.
        - **Blockchain:** Fondamentali per la sicurezza e l'immutabilità della catena.
    - Esempi noti: **MD5** (obsoleto per sicurezza ma ancora usato in alcuni contesti non critici), **SHA-1** (anche questo obsoleto per sicurezza), **SHA-256**, **SHA-512** (famiglia SHA-2), e più recenti come **SHA-3**.
## L'Importanza della Funzione Hash

La qualità di una funzione hash è cruciale per le prestazioni e la sicurezza delle strutture dati e dei sistemi che la utilizzano. Una funzione hash ben progettata garantisce rapidità nelle operazioni di ricerca e inserimento, mentre una funzione hash crittografica robusta è alla base della sicurezza di molte tecnologie digitali che usiamo ogni giorno.