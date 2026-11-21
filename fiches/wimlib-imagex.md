# wimlib-imagex — lire et extraire des archives WIM

**Couleur : orange.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Windows, macOS et analyse ; fenêtre `assistant-wimlib-imagex` ; terminal : `wimlib-imagex`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est la source protégée ; `sdY` une destination distincte. Pour l’analyse, préférer une copie ; ne jamais ouvrir l’original à récupérer avec `rescue-rw`. Les chemins en majuscules sont à remplacer après vérification.

## Usages

### 1. Capturer un dossier lisible — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
wimlib-imagex capture /mnt/SOURCE/Documents /mnt/DESTINATION/TRAVAIL/documents.wim DOCUMENTS --check
```

Le fichier WIM doit être neuf. Cela capture des fichiers, pas à lui seul une installation amorçable ni une image brute du disque.

### 2. Lire les images contenues dans un WIM — vert

```bash
wimlib-imagex info /mnt/ARCHIVES/documents.wim
```

Relever l’index de l’image avant extraction ; les noms et index appartiennent à cet exemplaire précis.

### 3. Appliquer une image dans un dossier neuf — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
mkdir /mnt/DESTINATION/TRAVAIL/extrait &&
wimlib-imagex apply /mnt/ARCHIVES/documents.wim 1 /mnt/DESTINATION/TRAVAIL/extrait --check
```

Remplacer 1 par l’index lu. Écrit dans extrait sur la destination, jamais dans le volume source ; les privilèges et métadonnées Windows peuvent nécessiter une procédure spécifique.

## Pièges

- Ne pas appliquer une image sur un système en service.
- Une vérification d’intégrité de l’archive ne certifie pas que son contenu est sain.

## Voir aussi

`sha256sum`, `ntfsclone`, guide 07.
