# Guida di Configurazione del Server Linux

Questa guida fornisce i passaggi necessari per configurare un server Linux con **Fail2ban**, **SSH**, **UFW** (firewall) e per installare **MySQL** e **PhpMyAdmin**. Segui questi passaggi per migliorare la sicurezza del tuo server e gestire i database in modo semplice ed efficiente.

---

## 🛠️ Installazione di Fail2ban

Fail2ban è uno strumento che protegge il server da attacchi di brute force monitorando i log e bannando gli IP malintenzionati.

### 1. Verifica la versione di Fail2ban
```bash
fail2ban-client --version

Copia il file di configurazione predefinito

sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local

3. Modifica il file di configurazione Apri l'editor di testo preferito per modificare jail.local:

sudo nano /etc/fail2ban/jail.local

🔐 Configurazione SSH
SSH è un servizio che permette l'accesso remoto al tuo server. Segui questi passaggi per configurarlo correttamente.

1. Installa OpenSSH

sudo apt install openssh-server

2. Avvia il servizio SSH

sudo systemctl start ssh

3. Abilita SSH all'avvio

sudo systemctl enable ssh

4. Verifica che SSH sia in esecuzione

sudo systemctl status ssh

5. Modifica la configurazione di SSH per aumentare la sicurezza

sudo nano /etc/ssh/sshd_config

Imposta una porta diversa da 22, disabilita l'accesso come root e aumenta la verbosità dei log con DEBUG.

6. Riavvia il servizio SSH

sudo systemctl restart ssh

🔥 Configurazione di UFW (Firewall) UFW è un firewall che aiuta a proteggere il server.

1. Controlla lo stato di UFW

sudo ufw status

2. Abilita UFW

sudo ufw enable

3. Blocca la porta 22 (se non usi SSH su questa porta)

sudo ufw deny 22/tcp

4. Imposta regole di traffico in entrata Blocca tutto il traffico in entrata tranne un IP specifico:

sudo ufw default deny incoming

sudo ufw allow from 192.168.200.122 to any port 3456 proto tcp

5. Consenti il traffico in uscita

sudo ufw default allow outgoing

6. Verifica lo stato di UFW

sudo ufw status verbose

🖥️ Installazione di MySQL e PhpMyAdmin

1. Installa MySQL

sudo apt install mysql-server -y

2. Avvia MySQL

sudo systemctl start mysql
3. Abilita MySQL all'avvio

sudo systemctl enable mysql

4. Installa PhpMyAdmin

sudo apt install phpmyadmin -y

5. Crea un link simbolico per PhpMyAdmin

sudo ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin

6. Riavvia Apache

sudo systemctl restart apache2

7. Accedi a PhpMyAdmin via browser

Vai su http://192.168.1.55/phpmyadmin nel tuo browser.

📊 Creazione di un Database MySQL
1. Accedi a MySQL

sudo mysql -u root -p

2. Crea un nuovo database


CREATE DATABASE ilmiodatabasecillone;

3. Crea un nuovo utente MySQL

CREATE USER 'alessandro'@'localhost' IDENTIFIED BY 'passwordforte';

4. Concedi privilegi all'utente sul database

GRANT ALL PRIVILEGES ON ilmiodatabasecillone.* TO 'alessandro'@'localhost';

5. Rendi effettive le modifiche

FLUSH PRIVILEGES;

🔐 Monitoraggio e Gestione Fail2ban
1. Verifica gli IP bannati

sudo fail2ban-client status sshd

🔧 Connessione SSH su Porta Personalizzata Se hai cambiato la porta SSH, puoi connetterti al tuo server usando il comando:

ssh -p 3456 server@192.168.200.122

Per una verbosità maggiore, usa il comando con -vvv:

ssh -vvv -p 3456 server@192.168.200.122
