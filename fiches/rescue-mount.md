# rescue-mount — monter sans rejouer de journal

**Couleur : vert.** Monte en lecture seule par défaut, sans exécuter les fichiers du disque.

**Lancer :** menu SOS, rubrique Partitions et volumes ; ou dans un terminal : `rescue-mount`.

Dans les exemples, remplacer `sdX` et les chemins en majuscules après identification avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. Les outils qui en ont besoin demandent automatiquement les droits sudo.

## Usages

### 1. Consulter une partition — vert

```bash
rescue-mount /dev/sdX1
```

Choisir la partition avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. Le dossier proposé est `/mnt/NOM` ; pour ext4, le journal n’est pas rejoué, donc les toutes dernières données peuvent manquer.

### 2. Ouvrir une image clonée — vert

```bash
rescue-mount /mnt/COPIE/disque.img
```

Attache l’image en lecture seule puis monte les systèmes reconnus. Une phrase de passe peut être nécessaire pour un volume chiffré.

### 3. Préparer une destination de copie — orange

```bash
lsblk -o NAME,SIZE,MODEL,SERIAL
rescue-rw /dev/sdX
rescue-mount --ecriture /dev/sdX1 /mnt/DESTINATION
```

Autorise les écritures sur la partition `/dev/sdX1` de la destination saine, jamais sur la source. Vérifier modèle, série et taille du disque parent, puis `findmnt /mnt/DESTINATION` avant d’y écrire.

### 4. Voir ce qui est ouvert — vert

```bash
rescue-mount --liste
```

Recense les montages et volumes gérés par cet outil avant de les refermer avec `rescue-umount`.

## Pièges

- Ne pas forcer un montage en écriture pour faire apparaître un journal manquant : travailler sur une copie.
- Ouvrir LUKS, LVM ou RAID crée des dépendances ; démonter avec `rescue-umount`, qui referme ce qu’il a ouvert.

## Voir aussi

`rescue-umount`, `rescue-ro`, `rescue-fsck`, guides 08 et 09.
