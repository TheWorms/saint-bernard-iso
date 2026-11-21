# smbclient — lire ou copier sans monter un partage

**Couleur : aucun.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Réseau ; fenêtre `assistant-smbclient` ; terminal : `smbclient`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une cible distincte, sacrifiable pour les effacements. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. `/tmp` et les rapports du live sont en RAM, perdus à l’arrêt. Un serveur distant doit être autorisé et son identité vérifiée.

## Usages

### 1. Lister un partage autorisé — aucun

```bash
smbclient //SERVEUR/PARTAGE -U UTILISATEUR -c 'ls'
```

Aucun montage ; le mot de passe est demandé. Ne pas utiliser de serveur extérieur dans le banc.

### 2. Télécharger vers le disque de destination — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
smbclient //SERVEUR/PARTAGE -U UTILISATEUR -c 'get lettre.txt /mnt/DESTINATION/TRAVAIL/lettre.txt'
```

Écrit uniquement la destination locale choisie ; choisir un nom neuf.

### 3. Envoyer un fichier récupéré — orange

```bash
smbclient //SERVEUR/PARTAGE -U UTILISATEUR -c 'put /mnt/COPIE/lettre.txt intervention-lettre.txt'
```

Écrit sur le partage autorisé, sans modifier la copie locale protégée.

## Pièges

- Ne pas placer le mot de passe après -U utilisateur%motdepasse ; le saisir au terminal.
- get écrit localement et put sur le serveur. Vérifier le partage et les deux chemins avant transfert.

## Voir aussi

`rescue-ro`, `rescue-rw`, `sha256sum`, guide 13.
