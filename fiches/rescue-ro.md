# rescue-ro — remettre un disque en lecture seule

**Couleur : vert.** Ne modifie aucune donnée : referme l’écriture ouverte par `rescue-rw`.

**Lancer :** menu SOS, rubrique Partitions et volumes ; ou dans un terminal : `rescue-ro`.

Dans les exemples, remplacer `sdX` et les chemins en majuscules après identification avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. Les outils qui en ont besoin demandent automatiquement les droits sudo.

## Usages

### 1. Voir les disques ouverts en écriture — vert

```bash
rescue-ro --liste
```

Affiche modèle et série des disques inscrits par `rescue-rw`. Si aucun n’est inscrit, affiche un message ; cela ne recense pas une ouverture manuelle avec `blockdev`.

### 2. Refermer un disque après une copie — vert

```bash
rescue-ro /dev/sdX
```

Le disque et ses partitions repassent en lecture seule. Choisir le disque avec `lsblk -o NAME,SIZE,MODEL,SERIAL` ; démonter d’abord toute partition montée en écriture.

### 3. Tout refermer avant de rendre la machine — vert

```bash
rescue-ro --tous
```

Referme aussi les disques passés en écriture à la main. Le disque qui porte `RESCUE-DATA` est laissé de côté pour conserver les journaux.

## Pièges

- Refus si une partition reste montée en écriture, sert de swap ou porte un volume RAID, LVM ou LUKS ouvert : démonter ou fermer d’abord.
- Un disque branché ensuite arrive protégé par les règles de l’image.

## Voir aussi

`rescue-rw`, `rescue-umount`, `rescue-mount` ; guides 00 et 08.
