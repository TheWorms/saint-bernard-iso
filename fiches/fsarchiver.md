# fsarchiver — archiver un système de fichiers sain

**Couleur : orange.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Clonage et images ; fenêtre `assistant-fsarchiver` ; terminal : `sudo fsarchiver`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est la source protégée ; `sdY` une destination distincte. Pour l’analyse, préférer une copie ; ne jamais ouvrir l’original à récupérer avec `rescue-rw`. Les chemins en majuscules sont à remplacer après vérification.

## Usages

### 1. Archiver une partition démontée — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
sudo fsarchiver savefs -j 2 /mnt/DESTINATION/TRAVAIL/partition.fsa /dev/sdX1
```

Lit une partition saine, démontée ; l’archive neuve est écrite sur un autre disque. Ne pas remplacer une image brute d’un disque défaillant par cette archive.

### 2. Lire le contenu déclaré de l’archive — vert

```bash
sudo fsarchiver archinfo /mnt/ARCHIVES/partition.fsa
```

Relever le numéro de système de fichiers pour une restauration ; lire les métadonnées n’est pas une restauration de contrôle.

### 3. Restaurer une partition de travail — rouge

```bash
rescue-rw /dev/sdY &&
sudo fsarchiver restfs /mnt/ARCHIVES/partition.fsa id=0,dest=/dev/sdY1
```

Écrase sdY1 démontée. id=0 doit correspondre au numéro lu avec archinfo ; la partition cible doit être suffisante et appartenir à un disque distinct de l’original.

## Pièges

- Ne pas sauvegarder un système de fichiers en écriture sans la procédure adaptée du guide.
- Une archive doit être essayée sur une cible de travail avant de compter sur elle.

## Voir aussi

`ddrescue`, `sha256sum`, guide 04.
