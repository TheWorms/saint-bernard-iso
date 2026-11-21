# blkdiscard — libérer les blocs d’une cible confirmée

**Couleur : rouge.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Effacement ; fenêtre `assistant-blkdiscard` ; terminal : `sudo blkdiscard`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une cible distincte, sacrifiable pour les effacements. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. `/tmp` et les rapports du live sont en RAM, perdus à l’arrêt. Un serveur distant doit être autorisé et son identité vérifiée.

## Usages

### 1. Libérer tout le disque confirmé — rouge

```bash
rescue-rw /dev/sdY &&
sudo blkdiscard --force --verbose /dev/sdY
```

Cible explicitement identifiée et entièrement sacrifiable ; aucune partition montée, aucun RAID/LVM actif dessus. Ce n’est pas une simulation.

### 2. Libérer une plage alignée — rouge

```bash
rescue-rw /dev/sdY &&
sudo blkdiscard --force --offset 1MiB --length 1MiB --verbose /dev/sdY
```

Détruit seulement cet intervalle d’exemple, sans comprendre les fichiers ; ce n’est pas un effacement complet du disque.

### 3. Demander un secure discard pris en charge — rouge

```bash
rescue-rw /dev/sdY &&
sudo blkdiscard --force --secure --verbose /dev/sdY
```

Exige le support matériel ; un refus ne justifie pas un autre effacement improvisé. Ne pas confondre avec ATA Secure Erase.

## Pièges

- Irréversible ; le contenu relu après TRIM n’est pas garanti nul. Le test sur boucle ne prouve pas l’effacement physique d’un SSD.
- --force supprime l’exclusivité : jamais pour contourner une cible montée ou occupée. Seulement après nom, taille et série confirmés, démontage et absence de détenteur ; nécessaire sur certains disques partitionnés.

## Voir aussi

`rescue-ro`, `rescue-rw`, `sha256sum`, guide 11.
