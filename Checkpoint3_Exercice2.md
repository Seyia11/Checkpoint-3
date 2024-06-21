# Exercice2

## Partie 1 : Gestion des utilisateurs

#### Q.2.1.1

![adduser](https://github.com/Seyia11/Checkpoint-3/blob/main/Capture/Exercice%201/Exercice%202/adduser.PNG?raw=true)

#### Q.2.1.2

Il est utile d'ajouter ce compte au groupe sudo et de définir un mdp complexe

```bash
usermod -aG sudo greg
```

## Partie 2 : Configuration de SSH

#### Q.2.2.1

```bash
nano /etc/ssh/sshd_config
```

Ajouter au fichier : ``PermitRootLogin no``

#### Q.2.2.2

Ajouter au fichier : ``AllowUsers greg``

#### Q.2.2.3

``PasswordAuthentication no`` et ``PubkeyAuthentication yes``

![pubkey](https://github.com/Seyia11/Checkpoint-3/blob/main/Capture/Exercice%201/Exercice%202/pubkey.PNG?raw=true)

Finir avec crt+o puis crt+x

## Partie 3 : Analyse du stockage

#### Q.2.3.1 

On utilise la commande ``lsblk`` et ``fdisk -l``

![lsblk](https://github.com/Seyia11/Checkpoint-3/blob/main/Capture/Exercice%201/Exercice%202/lsblk.PNG?raw=true)

- "/boot" monté sur md0p1 
- "/" monté sur cp3--vg-root
- "SWAP" monté sur cp3--vg-swap_1

#### Q.2.3.2

- md0p1 est en Raid1
- mdp05 est en LVM


#### Q.2.3.3

- Ajout d'un disque :

![disque](https://github.com/Seyia11/Checkpoint-3/blob/main/Capture/Exercice%201/Exercice%202/disque.PNG?raw=true)

- On vérifie que le disque sdb est bien présent (lsblk)
- vérifier l'état du RAID actuel : 
```bash
mdadm --detail /dev/md
```
Le Raid est en état dégradé

- Creer partition pour sdb

![partition](https://github.com/Seyia11/Checkpoint-3/blob/main/Capture/Exercice%201/Exercice%202/partition.PNG?raw=true)

- Refaire le Raid avec la partition sdb1 puis vérifier

![clean]( https://github.com/Seyia11/Checkpoint-3/blob/main/Capture/Exercice%201/Exercice%202/clean.PNG?raw=true)

####  Q.2.3.4

- voir les LV actuels -> lvdisplay et les groupe de volumes -> vgdisplay
- Créer LV de 2 GO
```bash
lvcreate -L 2G -n lv-new cp3-vg
```
- formater et monter

![mount](https://github.com/Seyia11/Checkpoint-3/blob/main/Capture/Exercice%201/Exercice%202/mount.PNG?raw=true)

- Montage automatique

![montage](https://github.com/Seyia11/Checkpoint-3/blob/main/Capture/Exercice%201/Exercice%202/montage.PNG?raw=true)

#### Q.2.3.5

Il reste 1.79 GO de libre.

![vgs](https://github.com/Seyia11/Checkpoint-3/blob/main/Capture/Exercice%201/Exercice%202/vgs.PNG?raw=true)


## Partie 4 : Sauvegardes

#### Q.2.4.1

- ``man bareos-dir`` 
Bareos Director, cette commande permet le paramétrage des sauvegardes.

- ``man bareos-sd``
Bareos's Storage, cette commande sert à définir l'emplacement des sauvegardes.

- ``man bareos-fd``
Bareos's File Daemon permet de réaliser des controles entre les sauvegardes et les fhichiers systèmes à sauvegarder.



## Partie 5 : Filtrage et analyse réseau

#### Q.2.5.1 

![nft](https://github.com/Seyia11/Checkpoint-3/blob/main/Capture/Exercice%201/Exercice%202/nft.PNG?raw=true)

- Les règles appliquées dans la table de filtrage concernent les flux en entrée (input).

#### Q.2.5.2

Les communications ci-dessous sont acceptées (input) :
- carte réseau lo
- protocole SSH sur port 22
- protocole de ping sur IPv4
- ping sur IPv6

#### Q.2.5.3 
- Aucune communication n'est interdite

#### Q.2.5.4

- fichier à editer ``config.nft``

![config](https://github.com/Seyia11/Checkpoint-3/blob/main/Capture/Exercice%201/Exercice%202/confignft.PNG?raw=true)

## Partie 6 : Analyse de logs

#### Q.2.6.1

```bash
cd /var/log
ls
```

![log](https://github.com/Seyia11/Checkpoint-3/blob/main/Capture/Exercice%201/Exercice%202/log.PNG?raw=true)

Je ne trouve pas le fichier qui contient les échecs de connexion.

Je pense qu'il faudrait éxecuter la commande ci dessous

```bash
grep 'failed login' fichierlog | tail -n 10
```

Je ne trouve rien dans les fichiers auth.log, lastlog et syslog.
