# Bluetooth e sicurezza
*Parleremo della tecnologia Bluetooth e di come viene gestita la sicurezza da questa tecnologia, quali sono le vulnerabilità, come proteggersi...*

## Indice
1. Introduzione al Bluetooth
2. Stack di protocolli Bluetooth
3. I protocolli di sicurezza nel Bluetooth Low Energy
4. I protocolli di sicurezza nel Bluetooth Classic
5. Vulnerabilità del Bluetooth
6. Attacchi noti
7. Come proteggersi
8. Conclusione

## Introduzione al Bluetooth
__Definizione__ : *Il Bluetooth è  una tecnologia di comunicazione wireless a corto raggio che consente lo scambio di dati tra dispositivi digitali.*

__Scopo__ : *Progettato per la comunicazione a bassa potenza e per la connessione di periferiche, sensori e altri dispositivi.*

__Diffusione__ : *Il Bluetooth lo troviamo ovunque , ad esempio in Smartphone, Tablet, Computer e laptop, Veicoli, Altoparlanti Bluetooth, Cuffie e auricolari wireless, Smartwatch,Dispositivi smart home....* 

Quindi, a differenza del modello ISO-OSI, il Bluetooth è progettato per dispositivi che comunicano sulla stessa frequenza, anziché all'interno della stessa rete. Tuttavia, entrambe le tecnologie utilizzano uno stack di protocolli.
Esistono due tecnologie di Bluetooth :  Low Energy(LE)  e Basic Rate/Enhanced data (BR/EDR)

Di conseguenza lo stack di protocolli è diverso tra le varie tecnologie, ma ovviamente in entrambe ci sono dei livelli che si dedicano alla sicurezza.

## Stack di protocolli Bluetooth
![image](https://github.com/user-attachments/assets/b5f0969a-9729-41c5-b3ae-feb05593e09c)

Per quanto riguarda il Bluetooth LE,  la sicurezza è gestita su più livelli dello **stack di protocollo**, ognuno con ruoli specifici, in particolare intervengono : LL,**SMP**,ATT,GATT

Per quanto riguarda invece il Bluetooth Classic , Il livello LMP è quello che si occupa anche di operazioni di sicurezza. 

In seguito spiegheremo questo adeguatamente

## Come viene gestita la sicurezza nel Bluetooth LE
### 1. Link Layer (LL) - Livello Controller  
- Implementa la **crittografia AES-CCM a 128 bit** per proteggere i dati trasmessi.  
- Gestisce **indirizzi MAC randomici** per la privacy e previene il tracciamento.  
- Previene attacchi **replay** usando nonce e contatori.  

### 3. Security Manager Protocol (SMP) - Pairing e Gestione Chiavi  
- Gestisce il **pairing**(riconoscimento) e la **distribuzione delle chiavi di sicurezza**.  
- Supporta diversi metodi di autenticazione, tra cui:  
  - **Just Works** (senza autenticazione)
  - **Passkey Entry** (uno dei dispositivi mostra un codice da inserire).  
  - **Numeric Comparison** (entrambi i dispositivi confrontano un codice).  
- Distribuisce chiavi come la **Long Term Key (LTK)** per la crittografia e la **Identity Resolving Key (IRK)** per la gestione della privacy.  

### 4. Attribute Protocol (ATT) e Generic Attribute Profile (GATT) - Livello Applicativo  
- **ATT** fornisce autenticazione e autorizzazione per l’accesso ai dati.  
- **GATT** definisce servizi e caratteristiche, alcuni dei quali possono richiedere **connessioni crittografate o autenticazione** per l’accesso.  

### 5. Secure Connections (Bluetooth 4.2 e successivi)  
- Introdotte con Bluetooth 4.2, usano **ECDH (Elliptic Curve Diffie-Hellman)** per uno scambio sicuro delle chiavi, migliorando la protezione contro attacchi MITM.  


## Come viene gestita la sicurezza nel Bluetooth Classic
- **LMP** gestisce il **pairing, l'autenticazione e lo scambio delle chiavi**.  
- **Baseband Layer** implementa la **crittografia e la protezione dai replay**.

## Vulnerabilità
- Debole autenticazione : il metodo di pairing Just Works non richiede autenticazione, quindi i dispositivi si accoppiano senza verificare la legittimità della comunicazione. Di conseguenza un attaccante potrebbe intercettare la comunicazione...
- non sempre gli indirizzi MAC vengono generati sufficientemente randomici
- AES  a 128 bit è una crittografia sicura. Ma lo è se le chiavi vengono generate e gestite correttamente. Quindi la gestione e protezione delle chiavi è fondamentale. Attraverso esse l' attacante può accedere a dati sensibili.
  - sono in circolazione dispositivi non aggiornati o obsoleti, inutilizzati ma col Bluetooth attivo che possono avere problemi risalenti ad anni fa

## Attacchi
- Sniffing : si intercettano i pacchetti di dati che vengono trasmessi in una comunicazione.
  Viene sfruttata la banda di frequenza che è aperta e non protetta, quindi attraverso  una sorta di ricevitori radio si riesce ad ascoltare la trasmissione.
  Durante il processo di pairing, sopratutto in metodi non sicuri come Just Works, si intercettano  i vari pacchetti grazie a applicazioni come Wireshark e è riusciti ad intercettare le comunicazioni.
  Si andranno quindi a sfruttare le vulnerabilità di crittografia, ecc per ottenere dati sensibili.
- Man in the Middle : un attaccante intercetta e manipla attivamente la comunicazione , agendo come intermediario.
  Viene prima fatto Sniffing, per raccogliere informazioni ma l' attaccante non si limità a ciò
  Modifica i dati in transito , falsifica messaggi, inietta comandi non autorizzati, può anche impersonare uno dei due dispositivi , facendo credere che la comunicazione sia reale...
QUesti due si trovano sopratutto nel Bluetooth LE

Ma esistono anche altri attacchi
- DoS : vengono inviati pacchetti di disturbo per interrompere la connessione Bluetooth di dispositivi
- Bluesnarfing : dati vengono rubati, grazie a tecniche viste in precedenza
- Bluebugging : un attaccante riesce a inviare attraverso il Bluetooth comandi che permettono di prendere il controllo del dispositivo che sta subendo l' attacco.
- Brute Force su Pin per comunicare via Bluetooth

## Come difendersi ? 
Noi utenti come facciamo a difenderci, ci sono alcune misure che è bene fare per essere più sicuri : 
1. Spegnere il Bluetooth se non lo usiamo
2. Non lasciare il dispositivo visibile , a meno che sia fondamentale
3. Usare PIN di configurazione Bluetooth sicuri
4. Diffidare da richiesta di pairing da dispositivi sconosciuti
5. Associazione tramite Bluetooth solo se esplicitato da noi. Non lasciare che ciò possa avvenire in automatico.


## Conclusione 

Abbiamo quindi visto cos' è il Bluetooth, quali livelli dello Stack Bluetooth si occupano di sicurezza e quali sono alcune problematiche che riguardano la sicurezza.


realizzato da Fusar Bassini Simone, Rosa Gabriele, Ingiardi Tommaso, Cornetti Andrea, Calabrese Alfredo.
4IC Telecomunicazioni 2024/2025 GALILEI CREMA
