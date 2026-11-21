# rescue-umount — refermer les montages et volumes

**Couleur : vert.** Démonte les ressources gérées par `rescue-mount`.

**Lancer :** menu SOS, rubrique Partitions et volumes ; ou dans un terminal : `rescue-umount`.

Dans les exemples, remplacer `sdX` et les chemins en majuscules après identification avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. Les outils qui en ont besoin demandent automatiquement les droits sudo.

## Usages

### 1. Démonter un dossier précis — vert

```bash
rescue-umount /mnt/DESTINATION
```

Fermer d’abord les fenêtres et terminaux qui utilisent ce dossier. Referme aussi les volumes ouverts pour lui quand ils ne servent plus.

### 2. Démonter à partir du périphérique — vert

```bash
rescue-umount /dev/sdX1
```

Choisir le périphérique dans `rescue-mount --liste`. Utile si le nom du dossier de montage a été oublié.

### 3. Tout refermer en fin d’intervention — vert

```bash
rescue-umount --tous
```

Démonte et referme tout ce que `rescue-mount` a ouvert. Ensuite, `rescue-ro --tous` retire les autorisations d’écriture.

## Pièges

- Un montage occupé doit être libéré avant de réessayer ; ne pas débrancher brutalement une destination.
- Démonter ne remet pas à lui seul le disque en lecture seule : terminer avec `rescue-ro`.

## Voir aussi

`rescue-mount`, `rescue-ro`, guide 08.
