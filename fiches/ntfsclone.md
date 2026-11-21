# ntfsclone — copier un NTFS sain

**Couleur : orange.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Clonage et images ; fenêtre `assistant-ntfsclone` ; terminal : `sudo ntfsclone`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est la source protégée ; `sdY` une destination distincte. Pour l’analyse, préférer une copie ; ne jamais ouvrir l’original à récupérer avec `rescue-rw`. Les chemins en majuscules sont à remplacer après vérification.

## Usages

### 1. Créer une image au format spécial ntfsclone — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
sudo ntfsclone --save-image --output /mnt/DESTINATION/TRAVAIL/ntfs.image /dev/sdX1
```

Source NTFS saine et démontée. Le format spécial décrit les blocs utilisés ; il n’est pas directement montable comme une image brute.

### 2. Restaurer le format spécial sur une partition — rouge

```bash
rescue-rw /dev/sdY &&
sudo ntfsclone --restore-image --overwrite /dev/sdY1 /mnt/ARCHIVES/ntfs.image
```

Écrase la partition sdY1, démontée et sacrifiable. Vérifier sa capacité et ne pas confondre --output fichier et --overwrite périphérique.

### 3. Créer une image brute creuse — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
sudo ntfsclone --output /mnt/DESTINATION/TRAVAIL/ntfs-brut.img /dev/sdX1
```

Sans --save-image, produit une image brute creuse. La destination doit prendre en charge les fichiers creux et garder assez d’espace réel.

## Pièges

- Ce n’est ni un outil de réparation ni un clonage tolérant les erreurs comme ddrescue.
- L’image d’une partition ne contient pas à elle seule tout l’amorçage du disque.

## Voir aussi

`ddrescue`, `losetup`, guide 04.
