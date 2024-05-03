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