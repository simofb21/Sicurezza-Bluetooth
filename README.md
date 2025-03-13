# Bluetooth e sicurezza
*Parleremo della tecnologia Bluetooth e di come viene gestita la sicurezza da questa tecnologia, quali sono le vulnerabilità, come proteggersi...*

## Indice
1. __***Introduzione al Bluetooth***__  Corne
2. __***Stack di protocolli Bluetooth***__  Corne
3. __***I protocolli di sicurezza nel Bluetooth Low Energy***__  Fius
4. __***I protocolli di sicurezza nel Bluetooth Classic***__  Rosa  
5. __***Vulnerabilità del Bluetooth***__  Fius
6. __***Attacchi noti***__ Ingio
7. __***Come proteggersi***__  Rosa
9. __***Conclusione***__  Alfredo

## Introduzione al Bluetooth
__Definizione__ : *Il Bluetooth è  una tecnologia di comunicazione wireless a corto raggio che consente lo scambio di dati tra dispositivi digitali.*

__Scopo__ : *Progettato per la comunicazione a bassa potenza e per la connessione di periferiche, sensori e altri dispositivi.*

__Diffusione__ : *Il Bluetooth lo troviamo ovunque , ad esempio in Smartphone, Tablet, Computer e laptop, Veicoli, Altoparlanti Bluetooth, Cuffie e auricolari wireless, Smartwatch,Dispositivi smart home....* 

Quindi, a differenza del modello ISO-OSI, il Bluetooth è progettato per dispositivi che comunicano sulla stessa frequenza, anziché all'interno della stessa rete. Tuttavia, entrambe le tecnologie utilizzano uno stack di protocolli.
Esistono due tecnologie di Bluetooth :  **Low Energy(LE)**  e **Basic Rate/Enhanced data (BR/EDR)**(classic)

Di conseguenza lo stack di protocolli è diverso tra le varie tecnologie, ma ovviamente in entrambe ci sono dei livelli che si dedicano alla sicurezza.

## Stack di protocolli Bluetooth
![image](https://github.com/user-attachments/assets/b5f0969a-9729-41c5-b3ae-feb05593e09c)

Per quanto riguarda il Bluetooth LE,  la sicurezza è gestita su più livelli dello **stack di protocollo**, ognuno con ruoli specifici, in particolare intervengono : LL,**SMP**,ATT,GATT

Per quanto riguarda invece il Bluetooth Classic , Il livello LMP è quello che si occupa anche di operazioni di sicurezza e anche il Baseband Layer. 

In seguito spiegheremo questo adeguatamente

## Come viene gestita la sicurezza nel Bluetooth LE
### 1. Link Layer (LL) - Livello Controller  
- Implementa la **crittografia AES-CCM a 128 bit** per proteggere i dati trasmessi.  
- Genera **indirizzi MAC randomici** per la privacy e previene il tracciamento.  
- Previene attacchi **replay**.  

### 2. Security Manager Protocol (SMP) - Pairing e Gestione Chiavi  
- definisce chi inizializza e chi risponde
- Gestisce il **pairing**(accoppiamento) e la **distribuzione delle chiavi di sicurezza**.  
- Supporta diversi metodi di autenticazione, tra cui:  
  - **Just Works** (senza autenticazione)
  - **Passkey Entry** (uno dei dispositivi mostra un codice da inserire).  
  - **Numeric Comparison** (entrambi i dispositivi confrontano un codice).  
- Distribuisce chiavi  per la crittografia e  per la gestione della privacy.  

### 3. Attribute Protocol (ATT) e Generic Attribute Profile (GATT) - Livello Applicativo  
- **ATT** fornisce autenticazione e autorizzazione per l’accesso ai dati.  
- **GATT** definisce servizi e caratteristiche, alcuni dei quali possono richiedere **connessioni crittografate o autenticazione** per l’accesso.  

### 4. Secure Connections (Bluetooth 4.2 e successivi)  
- Introdotte con Bluetooth 4.2, usano **ECDH (Elliptic Curve Diffie-Hellman)** per uno scambio sicuro delle chiavi, migliorando la protezione contro attacchi MITM.  


## Come viene gestita la sicurezza nel Bluetooth Classic
- **Baseband and Link Control** implementa la **crittografia e la protezione dai replay**:
   - appartiene al livello fisico
   - abilita il collegamento RF PHY tra i due dispositivi, formando una **PICONET**(rete dedicata a due o più dispositivi connessi tramite bluetooth)
   - **Baseband** gestisce l'elaborazione e la temporizzazione del canale
   - **Link control** controlla l'accesso al canale
   - crittografia basata sull'algoritmo **E0**
   - per la protezione dai replay si utilizza un contatore di frame, che cambia ad ogni trasmissione
   - due diversi tipi di connessione:
      - **sincrona**: traffico in tempo reale
      - **asincrona**: trasmissione di più pacchetti di dati
    
- **LMP** gestisce il **pairing, l'autenticazione e lo scambio delle chiavi**:
  - primo protocollo del livello collegamento
  - imposta la configurazione del collegamento tra i due dispositivi
  - inlude dei sistemi di sicurezza come autenticazione e crittografia con delle chiavi
  - controlla la modalità di alimentazione, i cicli di lavoro e gli stati di connessione
  - 3 modalità di sicurezza:
     - **1**: nessuna sicurezza
     - **2**: sicurezza a livello di servizio(politiche di sicurezza definite dall'applicazione
     - **3**: sicurezza a livello di collegamento
  - due versioni del pairing:
     - versioni vecchie usavano pairing basato sul PIN, vulnerabile ad attacchi
     - da Bluetooth 2.1+ introdotto SSP(secure simple pairing)

## Vulnerabilità
- **Debole autenticazione** : il metodo di pairing Just Works non richiede autenticazione, quindi i dispositivi si accoppiano senza verificare la legittimità della comunicazione. Di conseguenza un attaccante potrebbe intercettare la comunicazione...
- non sempre gli indirizzi MAC vengono generati sufficientemente randomici
- **AES**  a 128 bit è una crittografia sicura. Ma lo è se le **chiavi** vengono generate e gestite correttamente. Quindi la gestione e protezione delle chiavi è fondamentale. Attraverso esse l' attacante può accedere a dati sensibili.
- sono in circolazione dispositivi **non aggiornati o obsoleti**, inutilizzati ma col Bluetooth attivo che possono avere problemi risalenti ad anni fa

## Attacchi
- **Sniffing** : si intercettano i pacchetti di dati che vengono trasmessi in una comunicazione.
  Viene sfruttata la banda di frequenza che è aperta e non protetta, quindi attraverso  una sorta di ricevitori radio si riesce ad ascoltare la trasmissione.
  Durante il processo di pairing, sopratutto in metodi non sicuri come Just Works, si intercettano  i vari pacchetti grazie a applicazioni come Wireshark e è riusciti ad intercettare le comunicazioni.
  Si andranno quindi a sfruttare le vulnerabilità di crittografia, ecc per ottenere dati sensibili.
- **Man in the Middle** : un attaccante intercetta e manipla attivamente la comunicazione , agendo come intermediario.
  Viene prima fatto Sniffing, per raccogliere informazioni ma l' attaccante non si limità a ciò
  Modifica i dati in transito , falsifica messaggi, inietta comandi non autorizzati, può anche impersonare uno dei due dispositivi , facendo credere che la comunicazione sia reale...
  Questi due si trovano sopratutto nel Bluetooth LE
  ### Approfondimento Man in the Middle
> Ora che abbiamo visto cos è il MITM, adesso andremo a spiegare come funziona effettivamente...
>
> #### 1. Fase di riconoscimento e analisi
>
> L'attaccante inizia ascoltando passivamente le comunicazioni BLE nell'area:
>
> - Monitora lo spettro di frequenze Bluetooth (2.4 GHz)
> - Identifica i pacchetti di advertising dei dispositivi BLE attivi
> - Cataloga gli indirizzi dei dispositivi
> - Determina quali dispositivi stanno comunicando o potrebbero comunicare tra loro
>
> Durante questa fase, l'attaccante è completamente passivo e non altera in alcun modo la comunicazione.
>
> #### 2. Fase di clonazione e spoofing
>
> Per inserirsi tra due dispositivi, l'attaccante deve:
>
> - Creare due interfacce Bluetooth separate (una virtuale e una fisica)
> - Configurare la prima interfaccia per clonare il dispositivo peripheral:
>   - Copiare il l'indirizzo del dispositivo target
>   - Replicare esattamente i suoi pacchetti di advertising
>   - Simulare gli stessi servizi GATT
> - Configurare la seconda interfaccia per comunicare con il dispositivo  originale
> - Aumentare la potenza del segnale del clone per andare a "sostituire" il dispositivo originale.
>
> Il dispositivo centrale ora rileverà due dispositivi apparentemente identici, ma il clone dell'attaccante avrà un segnale più forte.
>
> #### 3. Fase di intercettazione della connessione
>
> Quando il dispositivo centrale tenta di connettersi:
>
> - Il dispositivo centrale si connette al clone (credendo sia il dispositivo legittimo)
> - Simultaneamente, l'attaccante si connette al dispositivo peripheral originale
> - L'attaccante crea così due canali di comunicazione separati:
>   ```
>   Dispositivo Centrale ↔ [Interfaccia 1 dell'attaccante] ... [Interfaccia 2 dell'attaccante] ↔ Dispositivo Peripheral
>   ```
> - Ogni messaggio viene ricevuto da una interfaccia e inoltrato all'altra
>
> #### 4. Intercettazione del processo di pairing
>
> Il momento cruciale è durante il pairing, quando vengono stabilite le chiavi di sicurezza:
>
> - L'attaccante intercetta la richiesta di pairing dal dispositivo centrale
> - Avvia un processo di pairing separato con il dispositivo peripheral
> - Durante lo scambio di chiavi pubbliche:
>   - Intercetta le chiavi pubbliche di entrambi i dispositivi
>   - Sostituisce queste chiavi con le proprie
>   - Stabilisce due canali crittografati separati (uno con ciascun dispositivo)
>
> Questo processo è particolarmente efficace nei metodi di pairing meno sicuri , quindi in Just Works
>
> #### 5. Manipolazione e relay del traffico
>
> Una volta stabilite le due connessioni, l'attaccante può:
>
> - **Relay passivo**: Semplicemente inoltrare i messaggi tra i due dispositivi
> - **Manipolazione attiva**: Modificare i dati prima di inoltrarli
> - **Inserimento**: Iniettare comandi o dati non inviati da nessuno dei dispositivi legittimi
> - **Blocco selettivo**: Impedire che certi messaggi raggiungano la destinazione
>
> #### 6. Meccanismi tecnici dell'attacco
>
> A livello di protocollo BLE, l'attacco funziona perché:
>
> - L'attaccante gestisce due connessioni distinte
> - **Nel Security Manager Protocol**: L'attaccante intercetta i messaggi di pairing e key exchange
> - **Nell'ATT/GATT**: L'attaccante può leggere e modificare tutti gli attributi scambiati

*fine approfondimento mitm*

Ma esistono anche altri attacchi
- **DoS** : vengono inviati pacchetti di disturbo per interrompere la connessione Bluetooth di dispositivi
- **Bluesnarfing** : dati vengono rubati, grazie a tecniche viste in precedenza
- **Bluebugging** : un attaccante riesce a inviare attraverso il Bluetooth comandi che permettono di prendere il controllo del dispositivo che sta subendo l' attacco.
- **Brute Force** su Pin per accoppiamento via Bluetooth

## Come difendersi ? 
Le ultime versioni di Bluetooth dalla 4.2 in poi sono più sicure.
Ma ci sono alcune pratiche che è bene seguire per noi utenti, per aumentare la nostra sicurezza:
1. Spegnere il Bluetooth se non lo usiamo per evitare **Bluebugging**, **Bluesnarfing** e **Bluejacking**
2. Non lasciare il dispositivo visibile , a meno che sia fondamentale
3. Usare PIN di configurazione Bluetooth sicuri e non banali o semplici
4. Diffidare da richiesta di pairing da dispositivi sconosciuti
5. Associazione tramite Bluetooth solo se esplicitato da noi. Non lasciare che ciò possa avvenire in automatico. Ablitiare anche SSP
6. Aggiornare il firmware del dispositivo
7. Evitare di usare bluetooth in luoghi pubblici affollati, per evitare attacchi di **sniffing**


## Conclusione 

Abbiamo quindi visto cos' è il Bluetooth, quali livelli dello Stack Bluetooth si occupano di sicurezza e quali sono alcune problematiche che riguardano la sicurezza.


realizzato da Fusar Bassini Simone, Rosa Gabriele, Ingiardi Tommaso, Cornetti Andrea, Calabrese Alfredo.
4IC Telecomunicazioni 2024/2025 GALILEI CREMA
