# rescue-recover — retrouver les fichiers sur une copie

**Couleur : orange.** PhotoRec écrit sur une autre destination ; TestDisk exige de la prudence.

**Lancer :** menu SOS, rubrique Récupération de fichiers ; ou dans un terminal : `rescue-recover`.

Dans les exemples, remplacer `sdX` et les chemins en majuscules après identification avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. Les outils qui en ont besoin demandent automatiquement les droits sudo.

## Usages

### 1. Extraire les fichiers avec PhotoRec — orange

```bash
rescue-recover photorec /mnt/COPIE/disque.img /mnt/DESTINATION/fichiers
```

Écrit les fichiers retrouvés sous `/mnt/DESTINATION/fichiers/recup_dir.N` sur un autre disque que celui de l’image. Après `rescue-rw` et montage de destination, contrôler `findmnt -T /mnt/COPIE/disque.img`, `findmnt /mnt/DESTINATION` et les modèles/séries avec `lsblk -o NAME,SIZE,MODEL,SERIAL`, puis choisir les types et le système de fichiers dans PhotoRec.

### 2. Rechercher les partitions avec TestDisk — rouge

```bash
rescue-recover testdisk /mnt/COPIE/travail.img
```

Une commande `Write` dans TestDisk modifie `travail.img` : utiliser seulement une copie de travail distincte de l’image de référence. Contrôler son chemin, son disque par modèle et série avec `findmnt -T /mnt/COPIE/travail.img` et `lsblk -o NAME,SIZE,MODEL,SERIAL` ; ouvrir le disque de copie par `rescue-rw` si une écriture est nécessaire.

### 3. Lire les options avant de commencer — vert

```bash
rescue-recover --help
```

Affiche l’aide de la commande sans agir sur un disque.

## Pièges

- Une destination en mémoire ou sur le disque source est refusée. Ne pas enregistrer les fichiers récupérés à côté de l’image si c’est le même disque.
- L’outil ne bloque pas tous les boutons de TestDisk : conserver l’original protégé et travailler sur une copie.

## Voir aussi

`rescue-clone`, `rescue-mount`, guide 06.
