# Creazione jar ed esecuzione App

Prima di tutto è necessario modificare il file sorgente DownloadGuardian.java, situato in "src/main/", aggiungendo la propria APIKey come stringa in modo da ottenere 
    
    private final String apikey = "------------------------";

con la propria API Key al posto dei trattini.

Requisiti per l'installazione

Assicurati che il tuo sistema soddisfi i seguenti requisiti:
- Java Development Kit (JDK) versione 8. 
- Apache Maven installato e configurato.
- Connessione Internet attiva.
- Spazio su disco sufficiente per i file scaricati.

### Compilare il progetto Maven

Per creare il file jar relativo al progetto e comprensivo delle dipendenze, dopo essersi posizionati nella cartella principale del progetto digitare:

    mvn package

Nella cartella "target/" verranno generati due file jar, di cui uno, (detto anche uber-jar) comprende anche tutte le dipendenze.


### Eseguire il progetto Maven

Per eseguire il progetto, dalla cartella principale, eseguire il comando:

    java -cp target/WordUsage-1-jar-with-dependencies.jar \
        it.unipd.dei.eis.fra.App

oppure

    java -jar target/WordUsage-1-jar-with-dependencies.jar

La seconda opzione utilizza direttamente la mainClass specificata nem pom.xml.

### Generare i javadocs

Per generare i javadocs

    mvn javadoc:javadoc

Le istruzioni per creare e rendere disponibile il maven site sono:

    mvn site
    mvn site:run

Il sito sarà quindi disponibile al seguente indirizzo: [http://localhost:8080/](http://localhost:8080/).
Se il collegamento tra il site e i javadocs dovesse dare errore, recarsi all'interno della cartella "target/site/" e selezionare i file da aprire.

### Panoramica del progetto

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

# Librerie e funzioni utilizzate

Gestione delle Richieste API e Download dei File:

-Libreria: Java Net
-Versione: Fornita dal JDK
-Funzione: Utilizzo di URL e HttpURLConnection per effettuare richieste HTTP alle API del Guardian e scaricare i file JSON degli articoli.

Elaborazione dei File JSON:

-Libreria: org.json
-Versione: 20160212
-Funzione: Utilizzata per analizzare e gestire i file JSON restituiti dall'API del Guardian, estrarre le informazioni necessarie e trasformarle in oggetti Java.

Analisi del Testo e Tokenizzazione:

-Libreria: Stanford CoreNLP
-Versione: 4.4.0
-Funzione: CoreNLP nella sua versione Simple è stata utilizzata nell'analisi del testo degli articoli scaricati per la tokenizzazione.

Lettura e Scrittura su File:

-Libreria: Java NIO (Native I/O)
-Versione: fornita dal JDK
-Funzione: Utilizzata per la creazione di JsonObject e l'accesso semplificato ai campi del Json. 

Conteggio delle Parole:

-Libreria: Java IO
-Versione: Fornita dal JDK
-Funzione: Utilizzata per gestire gli stream di scrittura/lettura verso/da file

Gestione dei Log:

-Libreria: Apache Log4j
-Versione: 2.0.7
-Funzione: Utilizzata per registrare eventi e messaggi durante l'esecuzione del programma, facilitando il debug e il monitoraggio.

Interazione con l'Utente da Linea di Comando:

-Libreria: Libreria Standard Java (java.util.Scanner)
-Versione: Fornita dal JDK
-Funzione: Utilizzata per interagire con l'utente da linea di comando, ad esempio per richiedere input o conferme.

Testing

-Libreria: JUnit
-Versione: 4.13.2
-Funzione: Utilizzata per i test
