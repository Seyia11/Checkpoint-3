# Exercice1

## Partie 1 : Gestion des utilisateurs

#### Q.1.1.1

Chercher le compte Kelly.Rhameur

```powershell
Get-ADuser Kelly.Rhameur
```
![kelly](https://github.com/Seyia11/Checkpoint-3/blob/main/Capture/Exercice%201/kelly.PNG?raw=true)

Ouvrir la console Active Directory Users ans Computeurs dans l'onglet Tools

Dans l'OU DirectionDesRessourcesHumaines, clic droit puis New -> User

![lionel](https://github.com/Seyia11/Checkpoint-3/blob/main/Capture/Exercice%201/lionel.PNG?raw=true)

mdp : Azerty1* puis cocher user must change password at next logon et finish



#### Q.1.1.2

- Créer OU à la racine du domaine TTSR.LAN
- Clic droit sur l'utilisateur Kelly puis Move

![desactived](https://github.com/Seyia11/Checkpoint-3/blob/main/Capture/Exercice%201/desactived.PNG?raw=true)

#### Q.1.1.3

- Clic droit sur l'utilisateur
- onglet member of
- selectionner GrpUsersDirectionDesRessourcesHumaines puis ``remove``


#### Q.1.1.4

![archive](https://github.com/Seyia11/Checkpoint-3/blob/main/Capture/Exercice%201/archive.PNG?raw=true)


## Partie 2 : Restriction utilisateurs

#### Q.1.2.1

- Chercher le compte Gabriel.Ghul

```powershell
Get-ADuser Gabriel.Ghul
```
L'utilisateur N'existe pas

essayer avec la commande
```powershell
Get-ADUser -Filter {Name -like "*Gabriel*"}
```
résultat Gabriel.Guhl

DistinguishedName : CN=Gabriel.Guhl,OU=Finance,OU=DirectionFinanciere,OU=LabUsers,DC=TSSR,DC=LAN

- Clic droit sur l'utilisateur puis properties
- Account -> Logon Hours

![Gabriel](https://github.com/Seyia11/Checkpoint-3/blob/main/Capture/Exercice%201/gabriel.PNG?raw=true)

- Apply


#### Q.1.2.2

- Clic droit sur l'utilisateur puis properties
- Account -> Logon To

![logon](https://github.com/Seyia11/Checkpoint-3/blob/main/Capture/Exercice%201/logon.PNG?raw=true)


#### Q.1.2.3

- Depuis le server manager 
- Tools -> Active Directory Administrative Center

![container](https://github.com/Seyia11/Checkpoint-3/blob/main/Capture/Exercice%201/container.PNG?raw=true)

- Clic droit -> New Password settings puis renseigner les champs
- Directly applies to : ajouter le groupe ``Domain User`` (on ne peut pas lier cette stratégie à l'OU LabUsers, par contre il est tout a fait possible de l'appliquer à un groupe et en l'occurence tous les utilisateurs font parties du groupe ``Domain User``)

![password](https://github.com/Seyia11/Checkpoint-3/blob/main/Capture/Exercice%201/password.PNG?raw=true)



## Partie 3 : Lecteurs réseaux

#### Q.1.3.1 

- Dans un premier temps il est nécessaire de partager les lecteurs E: et F: pour tous les utilisateurs en lecture :


![permission](https://github.com/Seyia11/Checkpoint-3/blob/main/Capture/Exercice%201/permission.PNG?raw=true)

Faire la meme maniplulation pour le lecteur f:


**_Dans le server manager_**

- Tools -> Group Policy Management
- Clic droit sur Group Policy Objects -> New -> Name : Users-Drive-Mount
- Clic droit edit
- User Configuration -> Preferences -> Windows Settings -> Drive Maps
- Clic droit -> New -> Mapped Drive

![Egeneral](https://github.com/Seyia11/Checkpoint-3/blob/main/Capture/Exercice%201/Egeneral.PNG?raw=true)

- Filtrer avec le groupe des utilisateurs

![groupe](https://github.com/Seyia11/Checkpoint-3/blob/main/Capture/Exercice%201/groupe.PNG?raw=true)

- Réaliser la meme configuration pour F:

![final](https://github.com/Seyia11/Checkpoint-3/blob/main/Capture/Exercice%201/final.PNG?raw=true)

- Dans la console Group Policy Management
- Onglet ``Details`` choisir ``Computer configuration settings disabled`` (uniquement pour les users) 
- Lié cette Gpo à l'OU LabUsers : Clic droit sur l'OU puis Link an Existing GPO

![OU](https://github.com/Seyia11/Checkpoint-3/blob/main/Capture/Exercice%201/OU.PNG?raw=true)


