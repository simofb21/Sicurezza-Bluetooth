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

Per quanto riguarda il Bluetooth LE , nel Controller Layer, la trasmissione può essere anche codificata, (con velocità 125 kbps nel Bluetooth 5.1) di conseguenza, già qua viene effettuata una prima cifratura delle informazioni.

In seguito però nell' Host Layer c'è un sottolivello che si occupa esclusivamente della sicurezza... l'SMP. 

Per quanto riguarda invece il Bluetooth Classic , Il livello LMP è quello che si occupa anche di operazioni di sicurezza. 

In seguito spiegheremo questo adeguatamente
