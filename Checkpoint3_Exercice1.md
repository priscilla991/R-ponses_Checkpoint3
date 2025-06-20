# Checkpoint 3 – Réponses

# Exercice 2 : Manipulations pratiques sur VM Linux (temps estimé : 2h30) 

### Partie 1 : Gestion des utilisateurs
### Q.2.1.1  
J’ai créé un compte personnel sur le serveur avec la commande **sudo adduser priscilla** (priscilla répresente le nom du compte à usage personnel que j'ai créé)

### Q.2.1.2  
Je recommande d’utiliser un mot de passe fort pour ce compte, de ne pas l’ajouter directement au groupe sudo sauf nécessité, et de désactiver la connexion SSH root pour privilégier l’authentification via ce compte utilisateur sécurisé.

### Partie 2 : Configuration de SSH
### Q.2.2.1  
Pour désactiver l'accès SSH au compte root, j’ai modifié le fichier **/etc/ssh/sshd_config** en décommentant la ligne **PermitRootLogin prohibit-password** et en remplacant la partie prohibit-password par **no**,pour obtenir **PermitRootLogin no** , puis j’ai redémarré le service SSH avec la commande **sudo systemctl restart sshd**.
![Capture d’écran du 2025-06-20 10-21-16](https://github.com/priscilla991/R-ponses_Checkpoint3/blob/main/Capture%20d%E2%80%99%C3%A9cran%20du%202025-06-20%2010-21-16.png)

### Q.2.2.2  
Pour restreindre l’accès SSH à mon seul compte personnel, j’ai ajouté la directive **AllowUsers priscilla** dans le fichier **/etc/ssh/sshd_config**, ce qui limite l’accès distant à l’utilisateur spécifié uniquement.  
![Capture d’écran du 2025-06-20 10-26-44](https://github.com/priscilla991/R-ponses_Checkpoint3/blob/main/Capture%20d%E2%80%99%C3%A9cran%20du%202025-06-20%2010-26-44.png)

### Q.2.2.3  
J’ai généré une paire de clés SSH avec **ssh-keygen** directement sur le serveur SRVLX01.
Ensuite, j’ai copié la clé publique **(id_rsa.pub)** dans le fichier **~/.ssh/authorized_keys** pour autoriser l’authentification par clé.
Enfin, j’ai vérifié les permissions et le contenu du fichier pour m’assurer que la configuration était correcte puis désactivé l’authentification par mot de passe dans **/etc/ssh/sshd_config** en mettant **PasswordAuthentication no**.  
![Capture d’écran du 2025-06-20 10-50-27](https://github.com/priscilla991/R-ponses_Checkpoint3/blob/main/Capture%20d%E2%80%99%C3%A9cran%20du%202025-06-20%2010-50-27.png)

### Partie 3 : Analyse du stockage  
### Q.2.3.1
Les systèmes de fichiers actuellement montés sont listés avec la commande **df -k**:  
/dev/mapper/cp3--vg-root monté sur /  
/dev/md0p1 monté sur /boot  et des systèmes temporaires en mémoire (tmpfs, udev) montés sur /dev, /run, /dev/shm, /run/lock et /run/user/0
![Capture d’écran du 2025-06-20 10-56-01](https://github.com/priscilla991/R-ponses_Checkpoint3/blob/main/Capture%20d%E2%80%99%C3%A9cran%20du%202025-06-20%2010-56-01.png)  

### Q.2.3.2
Le système principal utilise ext4 sur un volume LVM. Le répertoire /boot est sur une partition RAID.

### Q.2.3.3  
J’ai ajouté un nouveau disque de 8 Gio au serveur via l'interface graphique de VirtualBox au niveau du stockage (controleur SATA), créé une partition de type RAID avec **fdisk /dev/sdb**, puis je l’ai ajoutée au volume RAID **/dev/md0 avec mdadm --add /dev/md0 /dev/sdb1**. La reconstruction du RAID s’est lancée automatiquement et j'ai vérifié avec **cat /proc/mdstat**.
![Capture d’écran du 2025-06-20 12-06-01](https://github.com/priscilla991/R-ponses_Checkpoint3/blob/main/Capture%20d%E2%80%99%C3%A9cran%20du%202025-06-20%2011-29-46.png)

### Q.2.3.4
![Capture d’écran du 2025-06-20 12-06-01](https://github.com/priscilla991/R-ponses_Checkpoint3/blob/main/Capture%20d%E2%80%99%C3%A9cran%20du%202025-06-20%2012-06-01.png)

### Q.2.3.5
Il reste 6 Gio d’espace disponible dans le groupe de volume vg0, comme indiqué par la commande **vgdisplay**.

### Partie 4 : Sauvegardes

### Q.2.4.1

bareos-dir (Director) : C'est le chef d'orchestre. Il est responsable de la planification, du contrôle et du lancement des tâches de sauvegardes. Il contrôle l'ensemble des autres composants. Il est installé sur le serveur en charge de la gestion des sauvegardes.

bareos-sd (Storage Daemon) : Il gère le stockage physique des sauvegardes en recevant les données à enregistrer.

bareos-fd (File Daemon) : Installé sur les machines à sauvegarder, il envoie les fichiers au Storage Daemon sous le contrôle du Director.

### Partie 5 : Filtrage et analyse réseau
### Q.2.5.1
J'ai verifié les règles Netfilter actuellement avec la commande **nft list ruleset**

Le système utilise nftables et la politique par défaut est DROP.

### Q.2.5.2
les connexions établies ou relatives sont acceptées,

le trafic local (lo) est accepté,

les connexions SSH sur le port 22 sont autorisées,

le protocole ICMP (ping) est permis, ainsi que les paquets ICMPv6.

### Q.2.5.3
Tous les types de connexions non explicitement autorisés sont interdits, en raison de la politique par défaut drop. Cela peut inclure notamment :

tout le trafic entrant non établi ou non relié,

les connexions vers des ports autres que SSH (22),

les protocoles autres qu’ICMP et ICMPv6,

le trafic IPv4/IPv6 qui ne correspond à aucune règle "accept".

### Q.2.5.4
Pour permettre à Bareos de communiquer avec les clients sur le réseau local, j’ai ajouté les règles suivantes dans nftables :
**nft add rule inet inet_filter_table in_chain tcp dport {9101, 9102, 9103} accept**

### Partie 6 : Analyse de logs

### Q.2.6.1
Pour lister les 10 derniers échecs de connexion SSH, j’ai utilisé la commande:



