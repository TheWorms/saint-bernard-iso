# borg — sauvegarder et restaurer une archive chiffrée

**Couleur : orange.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Sauvegarde ; fenêtre `assistant-borg` ; terminal : `sudo borg`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une cible distincte, sacrifiable pour les effacements. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. `/tmp` et les rapports du live sont en RAM, perdus à l’arrêt. Un serveur distant doit être autorisé et son identité vérifiée.

## Usages

### 1. Initialiser un dépôt chiffré — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
sudo borg init --encryption=repokey-blake2 /mnt/DESTINATION/TRAVAIL/depot-borg
```

Dépôt neuf ; la phrase est saisie au terminal. La configuration et le cache du live disparaissent à l’arrêt.

### 2. Créer une archive nommée — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
sudo borg create --stats /mnt/DESTINATION/TRAVAIL/depot-borg::recup-AAAA-MM-JJ /mnt/COPIE/recuperation
```

Adapter le nom, conserver la source protégée et vérifier l’archive avant d’effacer quoi que ce soit.

### 3. Extraire dans un dossier neuf — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
mkdir /mnt/DESTINATION/TRAVAIL/restauration-borg &&
cd /mnt/DESTINATION/TRAVAIL/restauration-borg &&
sudo borg extract /mnt/ARCHIVES/depot-borg::recup-AAAA-MM-JJ
```

L’extraction écrit dans le dossier courant. Faire d’abord extract --dry-run, puis comparer les fichiers restaurés.

## Pièges

- La clé repokey et sa phrase de passe sont indispensables : exporter la clé dans un lieu distinct selon le guide.
- Le nom d’archive doit être neuf ; éviter delete/prune et toute restauration dans l’original.

## Voir aussi

`rescue-ro`, `rescue-rw`, `sha256sum`, guide 12.
