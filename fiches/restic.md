# restic — sauvegarder dans un dépôt chiffré

**Couleur : orange.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Sauvegarde ; fenêtre `assistant-restic` ; terminal : `sudo restic`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une cible distincte, sacrifiable pour les effacements. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. `/tmp` et les rapports du live sont en RAM, perdus à l’arrêt. Un serveur distant doit être autorisé et son identité vérifiée.

## Usages

### 1. Initialiser un dépôt distinct — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
sudo restic -r /mnt/DESTINATION/TRAVAIL/depot-restic init
```

Crée un dépôt neuf et demande son mot de passe au terminal. Ne pas réinitialiser un dépôt existant.

### 2. Sauvegarder les fichiers récupérés — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
sudo restic -r /mnt/DESTINATION/TRAVAIL/depot-restic backup /mnt/COPIE/recuperation
```

Dépôt initialisé et source stable en lecture seule. Un nouvel instantané est ajouté sans modifier la source.

### 3. Restaurer puis comparer — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
sudo restic -r /mnt/ARCHIVES/depot-restic restore latest --target /mnt/DESTINATION/TRAVAIL/restauration --verify
```

Restaurer dans un dossier neuf, jamais sur l’original. Comparer les fichiers connus ; latest doit désigner le bon instantané.

## Pièges

- Conserver le mot de passe et les clés hors du dépôt ; ne jamais les mettre dans la commande ni une capture.
- Un snapshot ne prouve pas une restauration ; vérifier le dépôt et extraire des fichiers. Ne pas lancer forget/prune pendant une récupération.

## Voir aussi

`rescue-ro`, `rescue-rw`, `sha256sum`, guide 12.
