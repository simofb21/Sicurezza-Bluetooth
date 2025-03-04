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
-**LMP** gestisce il **pairing, l'autenticazione e lo scambio delle chiavi**.  
- **Baseband Layer** implementa la **crittografia e la protezione dai replay**. 
