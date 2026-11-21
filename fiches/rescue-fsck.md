# rescue-fsck — vérifier avant de réparer

**Couleur : vert.** Simulation par défaut ; réparer est rouge et réservé à une copie.

**Lancer :** menu SOS, rubrique Systèmes de fichiers ; ou dans un terminal : `rescue-fsck`.

Dans les exemples, remplacer `sdX` et les chemins en majuscules après identification avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. Les outils qui en ont besoin demandent automatiquement les droits sudo.

## Usages

### 1. Vérifier une partition sans écrire — vert

```bash
rescue-fsck /dev/sdX1
```

La partition doit être démontée. Utilise le mode sans écriture du vérificateur adapté ; sur un disque entier, chaque partition reconnue est traitée.

### 2. Vérifier une image clonée — vert

```bash
rescue-fsck /mnt/COPIE/disque.img
```

Rattache l’image en lecture seule et vérifie son contenu. Préférer cette étape aux lectures répétées de l’original malade.

### 3. Réparer une copie de travail — rouge

```bash
rescue-fsck --reparer /mnt/COPIE/travail.img
```

Modifie `travail.img`, jamais l’image de référence ni le disque source. Vérifier le chemin et le disque qui le porte avec `findmnt -T /mnt/COPIE/travail.img` et `lsblk -o NAME,SIZE,MODEL,SERIAL` ; ouvrir ce disque avec `rescue-rw` si nécessaire, puis retaper le nom du fichier demandé.

## Pièges

- Jamais sur un système monté. La réparation d’une partition exige un disque de copie ouvert par `rescue-rw`.
- Pas de réparation Btrfs automatique ; récupérer les fichiers d’abord. `--oui` ne supprime pas la confirmation du nom.

## Voir aussi

`rescue-clone`, `rescue-umount`, guide 09.
