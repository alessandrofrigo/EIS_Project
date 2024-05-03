# Progetto EIS in Maven

Progetto di esame per il corso di Elementi di Ingegneria del Software.

Per compilare ed eseguire il progetto maven fare riferimento alla pagina [Eseguire il progetto](prj_exec.html).

Per informazioni sulle funzioni riutlizzate da altre librerie, andare alla pagina [Info sul progetto](prj_create.html).

# Panoramica del progetto

Il progetto è un'applicazione Java sviluppata per scaricare, analizzare e contare le parole più frequenti dagli articoli
ottenuti da The Guardian e da un file CSV. L'applicazione è suddivisa in tre classi principali: Analyze, Download, e App.

-Classe "Analyze" 

La classe è progettata per analizzare i file di testo presenti in una determinata cartella, estrarre le parole più frequenti e salvarle in un file di output. Ecco come funziona:

1. Utilizza la libreria Stanford Core NLP Simple per semplificare l'estrazione delle parole da un testo.
2. Definisce un metodo extractTerms() che prende il percorso di una cartella come input e analizza i file di testo all'interno.
3. Legge un elenco di parole vietate dal file "BanList.txt" e le memorizza in un insieme.
4. Estrae le parole da ogni file di testo, filtrando quelle vietate, e conteggia le parole uniche in base ai loro conteggi.
5. Utilizza il metodo sortByValue() per ordinare le parole in base alla loro frequenza.
6. Stampa le prime 10 parole più frequenti e le salva in un file "parolefrequenti.txt".

-Classe Astratta "Download"

La classe astratta Download fornisce un'infrastruttura comune per il download e l'archiviazione di articoli. I punti chiave sono i seguenti:

1. Definisce un metodo astratto downloadArticles() che dovrebbe essere implementato dalle sottoclassi per il download degli articoli.
2. Contiene un metodo storeArticles() che prende una lista di contenuti degli articoli e li archivia in file di testo all'interno di una cartella specificata.
3. Un metodo getFolder() viene utilizzato per ottenere il percorso della cartella specificata, creandola se non esiste già.
4. Utilizza il design pattern Template Method, dove il flusso generale del processo è definito nella classe base, mentre le sottoclassi ne implementano i dettagli specifici.

-Classe "DownloadGuardian"

La classe DownloadGuardian è una sottoclasse di Download ed è progettata per scaricare articoli da The Guardian. Le sue caratteristiche principali sono:

1. Definisce costruttori per configurare la query di ricerca.
2. Sovrascrive il metodo downloadArticles() per scaricare gli articoli da The Guardian utilizzando un'API key e una stringa di query.
3. Utilizza un loop per paginare attraverso i risultati e ottiene il corpo degli articoli dalla risposta JSON dell'API.

-Classe "DownloadNYT"

La classe DownloadNYT è una sottoclasse di Download e si concentra sul download di articoli da The New York Times (NYT) da un file CSV. Le sue caratteristiche principali includono:

1. Sovrascrive il metodo downloadArticles() per leggere gli articoli da un file CSV contenente articoli di NYT.
2. Effettua una lettura riga per riga del file CSV e estrae il corpo dell'articolo.
3. Gli articoli estratti vengono archiviati in una lista e restituiti dal metodo.
-Classe App 

Rappresenta il punto di ingresso dell'applicazione e offre un'interfaccia interattiva per selezionare azioni e sorgenti per il download ed estrazione dei termini dai testi. Di seguito le sue principali caratteristiche:

1. Utilizza la classe Scanner per ottenere l'input dell'utente.
2. Implementa un ciclo do-while per mantenere l'applicazione in esecuzione fino a quando l'utente decide di terminare il programma.
3. L'utente può selezionare tra tre azioni: solo download (DL), solo estrazione termini (EL) e download ed estrazione termini (DLEL).
4. L'utente può scegliere anche la sorgente: Guardian (G) o New York Times (NYT).
5. Per l'azione di download, crea istanze di DownloadGuardian o DownloadNYT a seconda della sorgente e richiama il metodo downloadAndStore() per scaricare e memorizzare gli articoli.
6. Per l'azione di estrazione termini, crea un'istanza di Analyze e chiama il metodo extractTerms() specificando la cartella di origine degli articoli.
7. L'azione di download ed estrazione termini combina le operazioni sopra menzionate.
8. Dopo ogni azione, viene chiesto all'utente se desidera eseguire un'altra operazione.

-Panoramica del Funzionamento

L'utente avvia il programma e interagisce con l'interfaccia utente. A seconda delle scelte effettuate,
l'applicazione scarica articoli da The Guardian o da un file CSV, li analizza per trovare le parole più frequenti, e mostra i risultati all'utente.
