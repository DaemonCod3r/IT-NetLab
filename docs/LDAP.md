# LDAP (Lightweight Directory Access Protocol) 
## Cos'è LDAP? 
LDAP (Lightweight Directory Access Protocol) è un protocollo usato per accedere e gestire informazioni in un directory service, una sorta di "rubrica" strutturata che contiene dati organizzati in modo gerarchico. È come una banca dati ottimizzata per leggere (più che scrivere) informazioni.

Ecco come funziona in parole semplici:  
### Cos'è un directory service?  
Un directory service è un sistema che memorizza informazioni su utenti, computer, gruppi e altri oggetti di una rete. Queste informazioni sono organizzate in una struttura ad albero. Ad esempio:  
* Alla radice c’è il dominio principale (ad esempio, "azienda.com").  
* Poi ci sono sottogruppi (come dipartimenti, gruppi di utenti, ecc.).
* Dentro ogni gruppo ci sono oggetti come utenti specifici.  

LDAP è il "linguaggio" standard che permette di cercare, leggere e modificare queste informazioni.
#### Facciamo un esempio pratico:
Immagina che un'azienda voglia controllare chi può accedere ad un’applicazione. Le informazioni su ogni dipendente (come nome utente, password, ruolo, email) sono salvate in un server che usa LDAP. Quando ti connetti al sistema, il tuo computer chiede al server LDAP:

"Chi è Mario Rossi? Ha il permesso di accedere?"
E il server LDAP risponde con i dati richiesti.  
### Cosa ci permette di fare?
* Autenticazione: Verifica chi sei (es. login su una rete aziendale).
* Autorizzazione: Decide cosa puoi fare (es. accedere a determinate risorse).
* Gestione centralizzata: Consente di gestire tutti gli utenti e risorse da un'unica posizione.

### Dove viene utilizzato?
LDAP viene utilizzato prevalentemente in:
* In ambienti aziendali per gestire utenti e accessi.
* In servizi web, per autenticare utenti con un'unica "rubrica".






