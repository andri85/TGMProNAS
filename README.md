## Novità — Versione 1.2-00202

### Banda modificabile durante i trasferimenti

Aggiunto il pulsante **Banda** nella coda delle operazioni per modificare il limite di upload e download senza interrompere il trasferimento.

- Limite indipendente per ogni operazione.
- Banda condivisa tra le connessioni parallele della stessa operazione.
- Impostazione conservata per pause, riprese e riavvio del servizio.
- Supporto ai trasferimenti di file durante backup e ripristino.
- Controllo dei permessi e validazione dei valori inseriti.

#### Utilizzo

1. Apri la coda delle operazioni.
2. Premi **Banda** accanto al trasferimento.
3. Inserisci il limite in **KiB/s** e conferma.

| Valore | Limite |
|---|---|
| `0` | Illimitato |
| `512` | 512 KiB/s |
| `1024` | 1 MiB/s |
| `10240` | 10 MiB/s |

Il limite si applica ai trasferimenti **NAS ↔ Telegram**. Non riguarda il caricamento browser → NAS, i trasferimenti cloud tramite rclone o gli inoltri interni a Telegram.

I blocchi già in rete possono completarsi prima che il nuovo limite abbia effetto. La velocità istantanea può mostrare brevi picchi.

### Pacchetti disponibili

| File | NAS supportato | Architettura |
|---|---|---|
| `TelegramManagerPro-DS218-DSM7-1.2-00202.spk` | Synology DS218 | ARM64 / rtd1296 |
| `TelegramManagerPro-Intel-x86_64-DSM7-1.2-00202.spk` | Synology con CPU Intel a 64 bit | x86_64 |

Entrambi i pacchetti includono le stesse funzioni e la versione di rclone per la rispettiva architettura.

### Requisiti

- DSM 7.0 o successivo.
- Python 3.8 o successivo con `sqlite3`, `ssl` e `asyncio`.

### Installazione e aggiornamento

1. Scarica il pacchetto adatto al tuo NAS.
2. Apri **Centro pacchetti → Installazione manuale**.
3. Seleziona il file `.spk` e completa l'installazione.
4. Per aggiornare, non disinstallare prima la versione precedente.
5. Ricarica la pagina dell'app dopo l'aggiornamento.

Apri Telegram Manager Pro dal menu DSM oppure visita:

`http://IP_DEL_NAS:8787/`

Non è necessario un reverse proxy.

### Verifiche

- Superati 8 test specifici del controllo banda.
- Superati 15 test di regressione.
- Superata la prova di avvio locale.
- Verificati struttura SPK, architetture degli eseguibili e collegamento del pulsante alla nuova API.

**Nota:** i trasferimenti dei test sono simulati. Installazione e prestazioni sui NAS reali restano da verificare.


# Telegram Manager Pro 1.2-00200

La versione è Telegram Manager Pro 1.2-00200, pacchetto aggiornato fix-porta-sessione, destinato al Synology DS218 con DSM 7.
Correzioni di questo pacchetto
- Icona nel menu DSM: apre l’app direttamente su HTTP, porta 8787, evitando il vecchio percorso sulla porta 5000.
- Sessione di accesso: usa cookie separati per protocollo e porta, evitando conflitti con quelli delle versioni precedenti.
- Verifica del login: controlla che il browser abbia conservato la sessione prima di entrare.
- Password: viene svuotata solo dopo l’accesso completato. Se manca il cookie, compare un messaggio specifico e puoi riprovare.
- Interfaccia: testi più chiari sulla distinzione tra accesso DSM e accesso all’app.
Funzioni mantenute
- Gestione account Telegram, chat e canali.
- Upload, download e code di trasferimento.
- Scansione canali, catalogo, ricerca e gestione duplicati.
- Cartelle sorvegliate, backup e collegamenti cloud tramite rclone.
- Tab per compilare le caption vuote, ad esempio fileName: $nomefile, con anteprima, filtri ed esportazione CSV. Questa funzione modifica la caption, non il nome del file allegato.
Accesso e limiti
L’indirizzo standard è http://x.x.x.x:8787/, senza reverse proxy. Il login al desktop DSM non autentica automaticamente l’app: devi inserire le credenziali DSM anche in Telegram Manager. La sessione dura 8 ore e termina se il servizio viene riavviato.
HTTPS diretto è configurabile, ma l’icona standard resta impostata su HTTP 8787. La modifica della banda durante i trasferimenti realizzata per l’edizione Windows non è inclusa in questa correzione NAS.
Verifiche: superati 15 test automatici e la prova del login con browser e server locali. L’autenticazione DSM era simulata: il funzionamento sul tuo NAS non è ancora confermato.

# Telegram Manager Pro

Gestore web per organizzare account Telegram, trasferire file tra Telegram e NAS, indicizzare canali e automatizzare gli upload.

| Informazione | Valore |
|---|---|
| Versione SPK | **1.1-00192** |
| Autore | **naplex19** |
| Data di creazione | **7 ottobre 2026** |
| NAS di destinazione | **Synology DS218** |
| Architettura | **rtd1296** |
| Sistema richiesto | **DSM 7.0 o superiore** |
| Runtime | **Python 3.8+**, con `sqlite3` e `ssl` |
| Identificativo pacchetto | `TelegramManager` |
| Accesso web | Reverse proxy HTTPS verso `127.0.0.1:8787` |

## Novità della versione 1.1-00192

- Cartelle NAS sorvegliate con caricamento automatico su Telegram.
- Un’unica barra di avanzamento per l’intera cartella o selezione in upload.
- Totale, trasferito e rimanente in GB/TB, percentuale ed ETA.
- Avanzamento cumulativo anche per i caricamenti dal browser al NAS.
- Conservati logo NAPLEX, caption automatiche, scansioni canali e registro operazioni.

## Accesso e account

- Autenticazione tramite credenziali DSM.
- Supporto al codice OTP DSM quando richiesto.
- Sessione web di otto ore.
- Password DSM non salvata dal programma.
- Gestione di più account Telegram per utente DSM.
- Collegamento tramite API ID, API Hash e numero di telefono.
- Accesso con codice Telegram e password 2FA.
- Sessioni Telegram persistenti.
- Selezione dell’account attivo.
- Nickname personalizzato per riconoscere l’account nel Manager.
- Verifica della connessione e dello stato Premium.
- Revoca della sessione Telegram.

> Il nickname è un alias locale: non modifica il nome pubblico o lo username `@` dell’account Telegram.

## Dashboard e chat

- Riepilogo dei file indicizzati e delle dimensioni.
- Conteggio delle operazioni attive.
- Visualizzazione della coda trasferimenti.
- Elenco e ricerca delle chat.
- Lettura dei messaggi e caricamento della cronologia precedente.
- Aggiornamento periodico dei messaggi.
- Invio di messaggi di testo.
- Visualizzazione delle informazioni dei media.
- Download dei media sul NAS.

## Upload dal browser al NAS

- Selezione di più file.
- Caricamento ricorsivo di cartelle.
- Trasferimento a blocchi.
- Barra cumulativa dell’intera selezione, senza azzeramento tra file.
- Visualizzazione di quantità trasferita e velocità.
- Tentativi automatici sui blocchi in caso di alcune interruzioni di rete.
- Conservazione dei nomi e delle sottocartelle ammessi.
- Segnalazione dei conflitti fra file omonimi, senza sovrascrittura automatica.

## Upload dal NAS a Telegram

- Selezione di file e cartelle dal percorso Upload.
- Scelta della chat di destinazione.
- Caption automatica con il nome effettivo dell’allegato.
- Testo aggiuntivo con segnaposto:
  - `{nome}`
  - `{indice}`
  - `{totale}`
- Anteprima indicativa della caption.
- Invio del testo senza interpretazione Markdown o HTML.
- Abbreviazione delle caption troppo lunghe.
- Invio senza suono di notifica.
- Compressione ZIP opzionale.
- Divisione automatica dei file oltre il limite implementato per l’account.
- Invio delle istruzioni per ricomporre le parti.
- Eliminazione delle selezioni sovrapposte dello stesso percorso nella medesima operazione.
- Scelta da 1 a 8 blocchi di upload paralleli.

### Avanzamento totale

La coda mostra una sola barra per ogni operazione di upload:

- Percentuale dell’intera cartella o selezione.
- Quantità totale da inviare.
- Quantità trasferita.
- Quantità rimanente.
- Dimensioni in GB/TB decimali.
- ETA stimato.
- Numero di allegati confermati.

Il totale viene determinato dopo la preparazione dei file. Per ZIP e divisioni comprende gli allegati effettivi da inviare.

L’ETA dipende dalla velocità corrente e non comprende compressione, divisione o attese imprevedibili di Telegram.

## Cartelle sorvegliate

Configurabili direttamente nella pagina **Upload**.

- Sorveglianza del percorso Upload o di una sua sottocartella.
- Ricerca ricorsiva nelle sottocartelle.
- Destinazione Telegram configurabile per ogni regola.
- Opzione per includere i file già presenti all’attivazione.
- Rilevamento dei file nuovi o modificati.
- Controllo indicativo ogni 30 secondi.
- Attesa di almeno 60 secondi senza variazioni di dimensione e data di modifica.
- Raggruppamento dei file pronti in operazioni da massimo 500 file.
- Caption automatica e divisione oltre limite attive negli upload automatici.
- Attivazione e disattivazione delle regole.
- Visualizzazione degli errori della cartella.
- Storico persistente per evitare riaccodamenti dello stesso percorso con identica dimensione e data.
- Controllo delle modifiche intervenute dopo la messa in coda.

Sono ignorati collegamenti simbolici, file e cartelle nascosti e file con estensione `.part`, `.tmp`, `.crdownload` o `.download`.

Ogni regola attende la conclusione della propria operazione prima di crearne un’altra. Operazioni in pausa o in errore richiedono intervento nella coda.

> La stabilità per 60 secondi non garantisce che una copia esterna sia terminata. Per copie che possono fermarsi a lungo, usare un nome `.tmp` e rinominarlo solo al termine.

La disattivazione ferma i nuovi accodamenti, ma non annulla quelli già creati. Il controllo dei file non è una deduplicazione per hash e non riconosce invii manuali o effettuati da altre regole.

## Download e verifica dei file

- Download da una chat o da un singolo ID messaggio.
- Limite opzionale dei messaggi da esaminare.
- Filtri per tipo, estensione, caption, dimensione e date.
- Limite di banda per operazione.
- Scelta da 1 a 8 blocchi di download paralleli.
- Organizzazione per account, chat e mese.
- File temporanei e ripresa dei download.
- Verifica della dimensione e calcolo SHA-256.
- File JSON con caption, data, autore, ID, sorgente e hash.
- Deduplicazione locale opzionale.

## Code e percorsi NAS

- Code persistenti in SQLite.
- Massimo due operazioni simultanee.
- Pausa, ripresa e annullamento.
- Stato, errori, velocità e fase corrente.
- Ripresa manuale delle operazioni interrotte da un riavvio.
- Percorsi Upload e Download personalizzabili.
- Cronologia dei percorsi.
- Permessi applicativi per le cartelle.
- Test di lettura, scrittura e rimozione.
- Conservazione del percorso assegnato alle operazioni già create.
- Selezione multipla ed eliminazione dei file locali.
- Protezione dei file coinvolti in trasferimenti non conclusi.

## Scansione canali e catalogo

### Modalità di scansione

- **Rapida:** esamina gli ultimi 1.000 messaggi accessibili.
- **Accurata:** esamina tutta la cronologia accessibile.
- Ripresa delle scansioni interrotte.
- Salvataggio di nomi, dimensioni, date, caption, tipi e riferimenti dei messaggi.
- Aggiornamento delle righe già indicizzate senza duplicarle.

### Elenco e ricerca

- Lista file scorrevole con intestazioni fisse.
- Nomi evidenziati e anteprima delle caption.
- Visualizzazione di dimensione, canale, data, autore, tipo e riferimento locale.
- Paginazione da massimo 100 file.
- Aggiornamento durante la scansione.
- Download selettivo dei risultati.
- Filtri per nome/caption, canale, date, autore, tipo o estensione.
- Filtri per tag, categoria e riferimento locale.

### Annotazioni ed esportazioni

- Tag e categorie personali.
- Modifica singola o multipla.
- Aggiunta, rimozione e sostituzione dei tag.
- Esportazione CSV.
- Esportazione JSON.
- Esportazione SQLite compresso.
- Esportazione di tutti i risultati filtrati, non soltanto della pagina corrente.

Le scansioni leggono i metadati: non scaricano né verificano il contenuto dei file. Le righe dei messaggi successivamente eliminati da Telegram restano nel catalogo.

## Video e player locale

- Invio come video dei file MP4, M4V e MOV con metadati riconosciuti.
- Lettura di dimensioni e durata senza ricodifica.
- Indicazione di streaming quando la struttura del contenitore lo consente.
- Invio come documento per i formati non riconosciuti.
- Anteprima audio/video dei file presenti sul NAS.

La riproduzione dipende dai codec e dal client utilizzato. I video suddivisi in parti devono essere ricomposti prima della riproduzione.

## Inoltro, sincronizzazione e cloud

- Inoltro di messaggi fra chat.
- Copia senza citazione quando consentita da Telegram.
- Caption sostitutiva per le copie.
- Filtri e selezione per ID messaggio.
- Regole sui nuovi messaggi per download o inoltro.
- Controllo delle regole di sincronizzazione ogni 30 secondi.
- Attivazione e disattivazione delle regole.
- Copia cloud opzionale dei download tramite rclone ARM64 incluso.
- Importazione di configurazioni WebDAV, FTP, SFTP, Mega, Google Drive e OneDrive.
- Copie cloud unidirezionali, senza cancellazione della destinazione.

Le autorizzazioni OAuth necessarie ai servizi cloud devono essere preparate esternamente.

## Backup, duplicati e statistiche

- Backup dei media sul NAS.
- Conservazione dei testi nell’indice.
- Ripristino verso una chat tramite nuovi invii.
- Ricerca dei file con SHA-256 identico.
- Riepilogo di nomi e caption dei duplicati.
- Cronologia delle modifiche alle caption nel database/API.
- Totali dell’indice e delle dimensioni.
- Conteggi per data e autore.
- File e byte trasferiti dal Manager.

Il ripristino non ricrea autori, ID, reazioni o risposte originali. Le statistiche non misurano i download effettuati da altri utenti Telegram.

## Canali, gruppi e moderazione

- Visualizzazione delle informazioni.
- Adesione e uscita.
- Creazione di canali e supergruppi.
- Modifica di titolo e descrizione.
- Invito, blocco e sblocco utenti.
- Modifica della foto del canale.
- Assegnazione dei diritti agli amministratori.
- Anteprima filtrata e conferma delle cancellazioni.
- Pulizia automatica fino a 100 messaggi ogni ora, esaminando gli ultimi 1.000.
- Filtri per anzianità e presenza di media.
- Parole bloccate nei testi inviati dal Manager.
- Blocco automatico opzionale in una chat configurata.

Le operazioni richiedono i relativi permessi Telegram e rispettano le restrizioni dei contenuti protetti.

## Log e diagnostica

- Casella di testo selezionabile con gli ultimi 500 eventi.
- Aggiornamento automatico ogni due secondi nelle pagine interessate.
- Pulsante di aggiornamento manuale.
- Pulsante **Pulisci log**, limitato al proprio utente.
- Registrazione di avvio, preparazione, invio, conferma, completamento ed errori.
- Diagnostica della versione, cifratura, connessione, concorrenza e timeout.

La pulizia del registro non elimina file, messaggi Telegram o operazioni in coda.

## Installazione

1. Verificare modello NAS, DSM e disponibilità di Python 3.8+ con `sqlite3` e `ssl`.
2. Conservare un backup dei dati e lasciare terminare gli invii attivi.
3. Aprire **Centro pacchetti → Installazione manuale**.
4. Selezionare `TelegramManagerPro-DS218-DSM7-1.1-00192.spk`.
5. Installare o aggiornare senza disinstallare la precedente versione.
6. Configurare il reverse proxy HTTPS.
7. Aprire il Manager, accedere con DSM e collegare Telegram.
8. Configurare i percorsi NAS e i permessi del servizio `TelegramManager`.
9. Ricaricare la pagina dopo ogni aggiornamento.

Il runtime Python non è incluso nello SPK.

## Reverse proxy

Esempio di configurazione:

| Parametro | Valore |
|---|---|
| Origine | HTTPS |
| Host origine | Nome DNS dedicato al Manager |
| Porta origine | 443 |
| Destinazione | HTTP |
| Host destinazione | `127.0.0.1` |
| Porta destinazione | `8787` |

Usare un certificato valido per il nome scelto. Il proxy deve conservare l’host pubblico e trasmettere `X-Forwarded-Proto: https`.

L’applicazione va aperta alla radice del dominio, senza sottopercorsi. La porta 8787 non deve essere esposta direttamente.

L’autenticazione DSM di questa versione utilizza internamente `http://127.0.0.1:5000`: tale servizio deve essere raggiungibile sul NAS.

## Dati e limiti

- Dati applicativi normalmente in `/var/packages/TelegramManager/var`.
- Database e impostazioni separati per utente DSM.
- Le cartelle NAS condivise restano soggette ai permessi DSM.
- Sessioni Telegram e API Hash protetti dai permessi dei file, ma non cifrati a riposo dal Manager.
- Nessuna funzione AI/OCR.
- Nessuna conversione video.
- Nessuna garanzia di velocità minima.
- Nessuna modifica retroattiva automatica delle caption già pubblicate.
- Nessuna notifica push di completamento implementata.

## Stato delle verifiche

La versione 1.1-00192 ha superato **18 test locali**, comprendenti regressioni upload, caption, log, scansioni, nickname e cartelle sorvegliate.

Verificati anche:

- Sintassi JavaScript.
- Barra unica dell’upload Telegram.
- Avanzamento cumulativo browser → NAS.
- Contenuti dell’archivio SPK.
- Permessi dei file eseguibili.

**Installazione DSM e trasferimenti reali su Telegram restano da collaudare sul NAS.**
