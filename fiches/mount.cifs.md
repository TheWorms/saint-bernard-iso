# mount.cifs — monter un partage SMB identifié

**Couleur : aucun.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Réseau ; fenêtre `assistant-mount.cifs` ; terminal : `sudo mount.cifs`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une cible distincte, sacrifiable pour les effacements. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. `/tmp` et les rapports du live sont en RAM, perdus à l’arrêt. Un serveur distant doit être autorisé et son identité vérifiée.

## Usages

### 1. Monter le partage en lecture seule — vert

```bash
sudo mkdir -p /mnt/RESEAU &&
sudo mount.cifs //SERVEUR/PARTAGE /mnt/RESEAU -o ro,vers=3.0,username=UTILISATEUR
```

Le point doit être vide ; vérifier findmnt et les fichiers connus avant usage.

### 2. Monter une destination réseau en écriture — orange

```bash
sudo mkdir -p /mnt/DEPOT &&
sudo mount.cifs //SERVEUR/PARTAGE /mnt/DEPOT -o rw,vers=3.0,username=UTILISATEUR
```

Seulement un partage autorisé et distinct de la source ; tester une copie puis la relire. Aucun disque physique local n’est ouvert en écriture par cette commande.

### 3. Démonter avant d’arrêter le serveur — vert

```bash
sudo umount /mnt/RESEAU
```

Sortir les terminaux de ce dossier et attendre la fin des copies ; ne pas masquer une erreur busy par un démontage forcé.

## Pièges

- Le montage RW écrit sur le serveur, pas dans un disque local protégé par rescue-ro. Obtenir le droit d’y déposer des données.
- Ne pas placer le mot de passe dans -o password= ; le saisir au terminal ou utiliser un fichier credentials privé hors des rapports.

## Voir aussi

`rescue-ro`, `rescue-rw`, `sha256sum`, guide 13.
