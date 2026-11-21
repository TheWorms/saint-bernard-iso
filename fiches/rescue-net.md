# rescue-net — utiliser une destination réseau

**Couleur : orange.** Les partages sont montés en écriture ; les disques locaux restent protégés.

**Lancer :** menu SOS, rubrique Réseau ; ou dans un terminal : `rescue-net`.

Dans les exemples, remplacer `sdX` et les chemins en majuscules après identification avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. Les outils qui en ont besoin demandent automatiquement les droits sudo.

## Usages

### 1. Examiner la connexion — vert

```bash
rescue-net etat
```

Affiche interfaces, adresses, DNS et réponse de la passerelle. Ne suppose pas qu’un accès Internet est disponible.

### 2. Monter une destination Samba — orange

```bash
rescue-net monter smb://SERVEUR/PARTAGE /mnt/RESEAU
```

Monte le partage distant en écriture sur `/mnt/RESEAU` : les copies iront sur le serveur, jamais sur la source locale. Vérifier le nom du serveur, le partage et `findmnt /mnt/RESEAU` ; pour une source disque, vérifier aussi modèle et série avec `lsblk -o NAME,SIZE,MODEL,SERIAL`.

### 3. Démonter les destinations réseau — vert

```bash
rescue-net demonter --tous
```

Fermer les fichiers et terminer les copies avant de démonter. Ne concerne que les montages gérés par `rescue-net`.

## Pièges

- Ne jamais placer un mot de passe dans la ligne de commande ; répondre à l’invite de l’outil.
- NFS et SSH sont aussi acceptés (`nfs://SERVEUR/CHEMIN`, `ssh://UTILISATEUR@HOTE/CHEMIN`). Tester place et permissions avant de lancer un clonage.

## Voir aussi

`rescue-clone`, `rescue-recover`, `rescue-ssh`, guide 13.
