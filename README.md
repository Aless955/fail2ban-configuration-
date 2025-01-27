installazione : 

sudo apt install fail2ban


verificare la versione : 

fail2ban-client --version

Fail2ban è dotato di file di configurazione predefiniti che puoi personalizzare in base alle tue esigenze. Il file di configurazione principale si trova in /etc/fail2ban/jail.conf .
Tuttavia, si consiglia di creare una copia locale ( /etc/fail2ban/jail.local ) per evitare che le modifiche vengano sovrascritte durante gli aggiornamenti. 
Il comando : 

sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local

apri un editor di testo che vuoi esempio nano,vim,ecc. :

sudo nano /etc/fail2ban/jail.local

 installare ssh 
ssh è un servizio che permette gli utenti di connettersi a una macchiana/pc/server da remoto : 
1) sudo apt install openssh-server 
2) sudo systemctl start ssh
3) sudo systemctl enable ssh
4) sudo systemctl status ssh ---→ visualizza se il servizio è in running

di norma l’ssh è la porta 22 ma cambiandola nel file di configurazione in ssh puoi mettere in sicurezza il server,eppure negare il login con root indispensabile, puoi aumentare la verbosità dei log con il DEBUG, il file di configurazione è : 
sudo nano /etc/ssh/sshd_config :

1) sudo systemctl restart fail2ban
2) sudo systemctl start fail2ban
3) sudo systemctl enable fail2ban
4) sudo systemctl status fail2ban


in ufw che sarebbe il firewall di linux abilitare il transito con di connessioni :

1) sudo ufw status --→ vedrà se il servizio è attivo se non lo è usare --→ sudo ufw enable 
2) abilitare la porta 3456 ---→ sudo ufw allow 3456/tcp
3) accesso in ssh sarà :  ssh -p 3456 server@192.168.200.122
oppure loggarsi con la verbosità  :

ssh -vvv -p 3456 server@192.168.200.122 o ssh -v -p 3456 server@192.168.200.122 
4) buttare giu la porta 22 : sudo ufw deny 22/tcp
5) se vuoi e se necessiti di tale cosa…. Bloccare tutto il traffico in entrata tranne per un solo IP a piacere. bloccare tutto il traffico in entrata :
sudo ufw default deny incoming
6) Consentire tutto il traffico in uscita:
sudo ufw default allow outgoing 
7)  Consenti l'accesso sulla porta 3456 solo dall'IP specifico :
sudo ufw allow from 192.168.200.122 to any port 3456 proto tcp  
8) verificare con la verbosità lo stato delle regole immesse :
sudo ufw status verbose
9) visualizzare gli ip bannati :
sudo fail2ban-client status sshd 


            fail2ban per myadmin e apache2
installazione apache2 e configurazione:
sudo apt install apache2 
attivazione servizi : 
sudo systemctl start apache2 
sudo systemctl status apache2 
sudo systemctl enable apache2 

accertarsi che funzioni :
http://192.168.1.55/
 installazione mysql / phpmyadmin: 
sudo apt install mysql-server -y
sudo systemctl start mysql
sudo systemctl enable mysql
installazione :
sudo apt install phpmyadmin -y

creare un link simbolico nel server web Apache per poterlo accedere facilmente via browser:
1) sudo ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin

2) sudo systemctl restart apache2

accesso al browser :
http://192.168.1.55/phpmyadmin

creazione database mysql : 
1) sudo mysql -u root -p
2) CREATE DATABASE ilmiodatabasecillone;
3) CREATE USER 'alessandro'@'localhost' IDENTIFIED BY 'passwordforte';
4) GRANT ALL PRIVILEGES ON ilmiodatabasecillone.* TO 'alessandro'@'localhost';
5) FLUSH PRIVILEGES;







