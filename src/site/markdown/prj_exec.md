# Creazione jar ed esecuzione App

Prima di tutto è necessario modificare il file sorgente DownloadGuardian.java, situato in "src/main/java/it/unipd/dei/eis/fra/", aggiungendo la propria APIKey come stringa in modo da ottenere 
    
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

Se per qualche motivo la compilazione di maven non dovesse andare a buon fine, è possibile scaricare il jar con le dipendenze da [https://drive.google.com/file/d/11Dki_tLHGw2GLa7DPCwgMM5yGSQFHZMH/view?usp=drive_link](Google Drive).
Scaricato il file, sarà necessario collocarlo nella cartella "target/" per passare all'esecuzione.

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
Se il collegamento tra il sito e i javadocs dovesse dare errore, recarsi all'interno della cartella "target/site/" e selezionare i file da aprire.
