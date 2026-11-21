# disktype — identifier les structures d’un support

**Couleur : vert.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Windows, macOS et analyse ; fenêtre `assistant-disktype` ; terminal : `sudo disktype`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est la source protégée ; `sdY` une destination distincte. Pour l’analyse, préférer une copie ; ne jamais ouvrir l’original à récupérer avec `rescue-rw`. Les chemins en majuscules sont à remplacer après vérification.

## Usages

### 1. Examiner un disque entier protégé — vert

```bash
sudo disktype /dev/sdX
```

Décrit tables et signatures reconnues sans les modifier ; recouper avec lsblk et mmls.

### 2. Examiner une partition — vert

```bash
sudo disktype /dev/sdX1
```

Une partition seule peut n’afficher qu’un système de fichiers ; l’absence de table à ce niveau est normale.

### 3. Examiner une image brute — vert

```bash
sudo disktype /mnt/COPIE/partition.img
```

Donner l’image brute, pas un qcow2 compressé ou un format spécial ntfsclone. Les signatures sont des indices, pas une réparation.

## Pièges

- Une signature peut être ancienne ou incohérente ; ne pas reformater pour obtenir un résultat plus clair.
- Cet outil ancien ne connaît pas nécessairement tous les formats récents.

## Voir aussi

`mmls`, `lsblk`, guide 07.
