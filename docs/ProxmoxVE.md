# ProxmoxVE
 Proxmox VE è una potente piattaforma di virtualizzazione server open-source per gestire due tecnologie di virtualizzazione – KVM (Kernel-based Virtual Machine) per le macchine virtuali e LXC per i container – con un’unica interfaccia web-based.  
 ## Installazione
 * 1. Il primo passo è scaricare l’immagine ISO di Proxmox VE dalla pagina ufficiale cliccando [QUI]("https://www.proxmox.com/en/downloads").  

 * 2. Il secondo step è quello di preparare il supporto USB,avremo bisogno di una chiavetta di almeno 2gb, scarichiamo [BalenaEtcher](https://etcher.balena.io/), e creiamo la nostra chiavetta con la iso di proxmox che abbiamo appena scaricato.  

 * 3. Ora possiamo installare ProxmoxVE nella macchina che andremo ad utilizzare come server,  
     - inseriamo la chiavetta nel nostro pc e accediamo al menù di avvio premendo l'apposito tasto (i più comuni sono Esc, F2, F10, F11 o F12.)  
    - Selezioniamo il supporto di installazione con l’immagine ISO Proxmox ed eseguiamo l’avvio da esso.  
    - Successivamente viene visualizzato il menu Proxmox VE.  
    - Selezionare Installa Proxmox VE per avviare l’installazione standard.
    - Accettiamo l’EULA con “I Agree” e proseguiamo.  
    - Nella pagina seguente ci verrà chiesto in quale disco installare proxmox (qui è possibile impostare eventuali raid) e clicchiamo su next.
    - Selezioniamo la timezone corretta ed il nostro layout di tastiera.
    - Nella schermata successiva andremo a creare l'account amminietratore e ad impostare la password.
    - Il passaggio finale nell’installazione di Proxmox è l’impostazione della configurazione di rete. Seleziona l’interfaccia di gestione, un nome host per il server, un indirizzo IP disponibile, il gateway predefinito e un server DNS.  
Il programma di installazione riassume le opzioni selezionate. Dopo aver confermato che tutto è in ordine, premi Installa. Al termine dell’installazione, rimuovere l’unità USB e riavviare il sistema.
Si può accedere al server anche tramite interfaccia web digitando l'IP del server e la porta 8006 https://IP:8006 le credenziali sono root e la password che abbiamo inserito durante l'installazione.  

## Configurazione dei Repository per gli aggiornamenti  
Proxmox di base è impostato per utilizzare repository per cui è necessario pagare un abbonamento, per utilizzare i repo gratuiti dobbiamo modificare un paio di file:  
apriamo con il nostro editor preferito (vim,nano) il file /etc/apt/sources.list commentiamo tutto il suo contenuto e aggiungiamo in fondo 
```bash 
deb http://ftp.debian.org/debian bookworm main contrib
deb http://ftp.debian.org/debian bookworm-updates main contrib

# Proxmox VE pve-no-subscription repository provided by proxmox.com,
# NOT recommended for production use
deb http://download.proxmox.com/debian/pve bookworm pve-no-subscription

# security updates
deb http://security.debian.org/debian-security bookworm-security main contrib
```  
poi andiamo a modificare anche il file /etc/apt/sources.list.d/ceph.list anche quì commentiamo tutto il contenuto e andiamo ad inserire in fondo:  
```bash 
deb http://download.proxmox.com/debian/ceph-squid bookworm no-subscription
``` 
adesso che abbiamo aggiunto i repo gratuiti possiamo restartare il server e aggiornare i pacchetti lanciando:  
```bash 
apt update && apt upgrade -y
``` 