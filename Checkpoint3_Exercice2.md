## Exercice 1 : Manipulations pratiques sur VM Windows (temps estimé : 1h30)

### Partie 1 : Gestion des utilisateurs

### Q.1.1.1  
Ouverture de la console Active Directory Users and Computers  
localiser l'utilsateur Kelly Rhameur  
Clique droit dessus ==> Copy.  
je renseigne les infos de Lionel Lemarchand et j'attribue un mot de passe.

![Création utilisateu Lionel Lemarchand](https://github.com/priscilla991/R-ponses_Checkpoint3/blob/main/Capture%20d%E2%80%99%C3%A9cran%20du%202025-06-23%2009-48-53.png)

### Q.1.1.2
Création de l'OU DeactivatedUsers + Deplacement du compte désactivé de l'utilisateur Kelly Rhameur  

![Création de l'OU DeactivatedUsers](https://github.com/priscilla991/R-ponses_Checkpoint3/blob/main/Capture%20d%E2%80%99%C3%A9cran%20du%202025-06-23%2009-59-12.png)

### Q.1.1.3  

Dans Active Directory Users and Computers, j'ai cherché les groupes de Kelly Rhameur  
Clique droit sur le groupe ==> Properties ==> onglet Members :  
J'ai Supprimé Kelly Rhameur, cliqué sur Add et ajouté Lionel Lemarchand  

![Modifier le groupe de l'OU dans laquelle était Kelly Rhameur ](https://github.com/priscilla991/R-ponses_Checkpoint3/blob/main/Capture%20d%E2%80%99%C3%A9cran%20du%202025-06-23%2010-21-33.png)

### Q.1.1.4

Dans explorateur de fichier, je suis allée dans le dossier individuel et j'ai créé le dossier de Lionel Lemarchand avec full control et ajouté le suffix ARCHIVE sur le nom du dossier de Kelly Rhameur.

![Création du dossier individuel de Lionel Lemarchand](https://github.com/priscilla991/R-ponses_Checkpoint3/blob/main/Capture%20d%E2%80%99%C3%A9cran%20du%202025-06-23%2010-39-25.png)

### Partie 2 : Restriction utilisateurs

### Q.1.2.1   

Dans AD Users and Coputers, je suis allée à :  
Onglet Account ==> cliquer sur Logon Hours, Sélectionné lundi à vendredi, de 07:00 à 17:00 ==> cliqué sur Logon Permitted.  
Sur le reste ==> Logon Denied.  
Valider avec OK.  

![capture d'écran](https://github.com/priscilla991/R-ponses_Checkpoint3/blob/main/Capture%20d%E2%80%99%C3%A9cran%20du%202025-06-23%2010-57-43.png)

### Q.1.2.2   

Toujours dans Properties de Gabriel Ghul ==> onglet Account ==> Log on to  
Cocher The following computers.  
Ajouter : CLIENT01.  
Valide.  

![capture d'écran](https://github.com/priscilla991/R-ponses_Checkpoint3/blob/main/Capture%20d%E2%80%99%C3%A9cran%20du%202025-06-23%2011-00-49.png)

### Q.1.2.3 

![capture d'ecran](https://github.com/priscilla991/R-ponses_Checkpoint3/blob/main/Capture%20d%E2%80%99%C3%A9cran%20du%202025-06-23%2011-38-08.png)

### Partie 3 : Lecteurs réseaux

### Q.1.3.1 Créer une GPO Drive-Mount qui monte les lecteurs E: et F: sur les clients.

![capture d'ecran](https://github.com/priscilla991/R-ponses_Checkpoint3/blob/main/Capture%20d%E2%80%99%C3%A9cran%20du%202025-06-23%2011-47-21.png)

![capture d'écran](https://github.com/priscilla991/R-ponses_Checkpoint3/blob/main/Capture%20d%E2%80%99%C3%A9cran%20du%202025-06-23%2011-50-20.png)




