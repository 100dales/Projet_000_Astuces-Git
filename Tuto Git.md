# Astuce Git / GitHub

## Configurer votre Git avant de commencer à travailler

Afin d'utiliser Git, il te faut l'installer https://git-scm.com/downloads
Sur Windows, tu peux tout laisser par défaut !

### Configuration utilisateur
```
git config --global user.name "100dales"
git config --global user.email 100dales@example.com
```
### Configuration des couleurs
```
git config --global color.diff auto
git config --global color.status auto
git config --global color.branch auto
```
### Création du dépôt local
Pour se faire, créé un dossier (en local / sur ton PC) comme, */Documents/Projets/DossierDeMonProjet1*
### Initialise ton dépôt local
```
cd /Documents/Projets/DossierDeMonProjet1
git init
```
### Relier le dépôt local au dépôt distant (créé au préalable sur GitHub)
```
git remote add origin https://github.com/100dales/DossierDeMonProjet1.git
git branch -M main
git push -u origin main
```

## Travailler dans le dépôt local

### Le Working directory (WD)
Cette zone correspond au dossier du projet sur votre ordinateur.
Pour passer un fichier du WD au stage :
```
git add NomDuFichier
```
### Le Stage ou index
Cette zone est un intermédiaire entre le working directory et le repository. Elle représente tous les fichiers modifiés que vous souhaitez voir apparaître dans votre prochaine version de code.
Pour passer un fichier de Stage au Repository
```
git commit -m "message particulier rattaché au commit effectué"
```
### Le Repository
Lorsque l’on crée de nouvelles versions d’un projet, c’est dans cette zone qu’elles sont stockées.
```
git push origin main
```

## Système de branche
Les différentes branches correspondent à des copies de votre code principal à un instant T, où vous pourrez tester toutes vos idées sans que cela impacte votre code principal.
Sous Git, la branche principale est appelée la branche "main" ("master" pour les dépôts créés avant octobre 2020). 

La branche principale portera l’intégralité des modifications effectuées. Le but n’est donc pas de réaliser les modifications directement sur cette branche, mais de les réaliser sur d’autres branches, et après divers tests, de les intégrer sur la branche principale.

### Connaître les branches présentes dans notre projet
```
git branch
```
L’étoile signifie que c’est la branche sur laquelle vous vous situez
### Créer une branche
```
git branch NomDeMaBranche
```
### Changer de branche
```
git checkout NomDeMaBranche
```
### Supprimer une branche
```
git branch -d NomDeMaBranche
```
ou si il y a déjà eu des modifications dans la branche
```
git branch -D NomDeMaBranche
```

## Fusionner le travail effectué sur la branche avec le main
Repasser sur "main"
```
git checkout main
```
Fusionner votre branche "NomDeMaBranche" au "main"
```
git merge NomDeMaBranche
```

## Travaillez avec un dépôt distant

### Accéder à un dépôt distant et le copier en local
Cloner le Repository distant
```
git clone https://github.com/100dales/DossierDeMonProjet2.git
```
### Le nom du dossier est trop long ?
```
git remote add NouveauNomPlusCourt https://github.com/100dales/DossierDeMonProjet2.git
```
### Mettre à jour le dépôt local
```
git pull NouveauNomPlusCourt main
```



## J'ai modifier la branche "main" par erreur
Si vous avez modifié votre branche principale avant de créer votre branche et que vous n'avez pas fait le commit, ce n’est pas bien grave. Il vous suffit de faire un stash (remise) en anglais.

### Vérifier le statut des fichiers
```
git status
```
### Créer un stash
```
git stash
```
### Créer la branche voulue et y aller et appliquer la remise (stash)
```
git branch MaNouvelleBranche
git checkout MaNouvelleBranche
git stash apply
```
### Si il y a plusieurs stash en cours
```
git stash list
git stash apply stash@{0}
```



## J’ai modifié la branche après avoir fait un commit

### Vous allez alors récupérer l'identifiant du commit que l'on appelle couramment le hash. 
```
git log commit
```
### Supprimer de la branche principale votre dernier commit
Maintenant que vous disposez de votre identifiant, gardez-le bien de côté. Vérifiez que vous êtes sur votre branche principale et réalisez la commande suivante :
```
git reset --hard HEAD^
```
Le HEAD^ indique que c'est bien le dernier commit que nous voulons supprimer. L’historique sera changé, les fichiers seront supprimés.
### Créez ensuite votre nouvelle branche.
```
git branch MaNouvelleBranche
```
### Vous allez basculer sur cette branche.
```
git checkout MaNouvelleBranche
```
### Appliquer ce commit sur votre nouvelle branche
```
git reset --hard 8PremiersCaractèresDuHash
```

## Corriger les erreurs en local et à distance
Il est possible d'annuler son commit public (git push) avec la commande git revert. L'opération revert annule un commit en créant un nouveau commit. C'est une méthode sûre pour annuler des changements, car elle ne risque pas de réécrire l'historique du commit.
```
git revert HEAD^
```

## L'accès à distance ne fonctionne pas
Générer une nouvelle clé SSH
```
ssh-keygen -t rsa -b 4096 -C "100dales@example.com"
```
Aller recherche le dossier contenant la clé SSH publique (sur votre ordianteur) et la mettre dans GitHub

Lien : https://openclassrooms.com/fr/courses/7162856-gerez-du-code-avec-git-et-github/7165666-corrigez-vos-erreurs-sur-votre-depot-distant#/id/video_Player_2

## Revenir en arrière

### Git reset permet de revenir à l'état précédent sans créer un nouveau commit (préférer --mixed, pour --hard vérifer 15 fois et être sûr à 200%)
```
git reset notreCommitCible --soft
git reset notreCommitCible --mixed
git reset notreCommitCible --hard
```
### Git revert permet de revenir à l'état précédent en créant un nouveau commit.
```
git revert HEAD
```
Le HEAD est un pointeur, une référence sur votre position actuelle dans votre répertoire de travail Git.

## Journal de log Git
```
git log
git reflog
```

## Examiner le contenu d'un fichier
Vous découvrez un bug dans votre projet, vous allez avoir besoin d'identifier son origine et de savoir qui a modifié chaque ligne du code.
```
git blame monFichier.php
```

