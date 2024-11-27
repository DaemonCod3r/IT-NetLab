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
**Facciamo un esempio pratico:**
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

# Come si configura?  
Iniziamo la parte divertente...(forse 😈) proviamo a configurare un server con LDAP.  
Requisiti: 
* Avere un Server/home-Server Tutorial [ProxmoxVE](https://) 
* VM con Ubuntu 24.04 server [Ubuntu-Server](https://)  

Nella guida utilizzeremo tutti i comandi relativi a Ubuntu24.04 LTS. 
Per prima cosa connettiamoci alla macchina remota  
```bash 
ssh host@ip 
```
aggiorniamo i pacchetti  
```bash 
sudo apt update && sudo apt upgrade -y
```
una volta fatti gli aggiornamenti andiamo ad 
installare i pacchetti di cui avremo bisogno.  
Iniziamo installando [Apache](https://) e tutte le sue dipendenze.  
```bash 
sudo apt install apache2 php php-cgi libapache2-mod-php php-mbstring php-common php-pear -y
```
Una volta installato il webserver andiamo ad installare OpenLDAP Server.  
```bash 
sudo apt install slapd ldap-utils -y
```
Per finire installiamo LDAP Account Manager, non è altro
che un'interfaccia web per poter gestire in maniera semplice e comoda
le varie voci memorizzate nella nostra LDAP  
```bash 
sudo apt -y install ldap-account-manager
```
abilitiamo l'estensione di php chiamata php-cgi  
```bash 
sudo a2enconf php*-cgi
```
l'asterisco "*" serve per non dover inserire la versione di php.  
Restartiamo Apache  
```bash 
sudo systemctl reload apache2
```
Abilitiamo l'autostart di apache all'avvio della VM  
```bash 
sudo systemctl enable apache2
```
controlliamo che apache sia partito senza problemi:  
```bash 
sudo systemctl status apache2
```
ora possiamo configurare LDAP Account Manager 
connettendoci al seguente indirizzo  
```bash 
http://<ip della VM>/lam
```
clicchiamo su "LAM Configuration" in alto a destra poi su 
"Edit server profiles", inseriamo la password di default "lam"
e clicchiamo su ok.  
Da qui possiamo cambiare la lingua e la timezone.  

**ATTENZIONE!!!! non modificare il server address.**  

Nella sezione "tool settings" possiamo modificare il tree suffix con quello della nostra rete
se ad esempio la nostra rete è host.home.lan andremo a modificare i campi nel seguente modo
dc=home,dc=lan  

Nella sezione "Security settings" (attenzione potrebbe trovarsi nella sezione "server settings" con gli ultimi aggiornamenti.) modifichiamo list of valid users inserendo 
cn=admin,dc=home,dc=lan  

Per finire andiamo a cambiare le password con una a nostra scelta e clicchiamo su "salva".  

Ora torniamo nella sezione da cui siamo appena usciti ma questa volta per accedervi dobbiamo inserire la password
che abbiamo appena creato e non più quella di default "lam".  
  
Clicchiamo sulla scheda in alto "Account types".
