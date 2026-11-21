# rescue-boot-repair — diagnostiquer et réparer le démarrage

**Couleur : rouge.** Le diagnostic lit seulement ; GRUB modifie la copie de travail.

**Lancer :** menu SOS, rubrique Démarrage et Windows ; ou dans un terminal : `rescue-boot-repair`.

Dans les exemples, remplacer `sdX` et les chemins en majuscules après identification avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. Les outils qui en ont besoin demandent automatiquement les droits sudo.

## Usages

### 1. Diagnostiquer sans écrire — vert

```bash
rescue-boot-repair diagnostic /dev/sdX
```

Lit table, amorces et fichiers Linux utiles sans rejouer les journaux. Les constats indiquent la suite ; ils ne réparent rien.

### 2. Sauvegarder avant toute réparation — orange

```bash
rescue-boot-repair sauvegarde /dev/sdX /mnt/DESTINATION
```

Écrit `demarrage-sdX-DATE` sur la destination montée après `rescue-rw`. Contrôler modèle et série des deux disques avec `lsblk -o NAME,SIZE,MODEL,SERIAL` et `findmnt /mnt/DESTINATION` : la sauvegarde ne doit pas être sur `/dev/sdX`.

### 3. Réinstaller GRUB BIOS sur la copie — rouge

```bash
lsblk -o NAME,SIZE,MODEL,SERIAL
rescue-rw /dev/sdX
rescue-boot-repair grub /dev/sdX /dev/sdX1 /mnt/DESTINATION
```

Écrit l’amorce de `/dev/sdX` et les fichiers GRUB du Linux de `/dev/sdX1`, après sauvegarde sur un autre disque. Choisir la copie par modèle et série, remplacer aussi la partition racine, puis retaper son nom ; jamais l’original ni le support live.

## Pièges

- Ne répare pas automatiquement UEFI, NVRAM ni le BCD Windows : suivre le guide 10.
- La partition racine montrée est un exemple ; ne pas supposer que la première partition est la bonne.

## Voir aussi

`rescue-clone`, `rescue-rw`, `rescue-ro`, guide 10.
