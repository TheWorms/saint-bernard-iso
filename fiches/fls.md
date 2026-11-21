# fls — lister les entrées d’un système de fichiers

**Couleur : vert.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Récupération de fichiers ; fenêtre `assistant-fls` ; terminal : `sudo fls`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est la source protégée ; `sdY` une destination distincte. Pour l’analyse, préférer une copie ; ne jamais ouvrir l’original à récupérer avec `rescue-rw`. Les chemins en majuscules sont à remplacer après vérification.

## Usages

### 1. Lire le premier niveau d’une image partitionnée — vert

```bash
sudo fls -o 2048 /mnt/COPIE/disque.img
```

2048 est un exemple de décalage en secteurs : le relever avec mmls. fls attend le début du système de fichiers.

### 2. Parcourir les répertoires récursivement — vert

```bash
sudo fls -r -o 2048 /mnt/COPIE/disque.img
```

Affiche noms et inodes pour l’analyse ; cela n’extrait pas les contenus et ne valide pas les fichiers.

### 3. Afficher les entrées supprimées d’une image de partition — vert

```bash
sudo fls -d /mnt/COPIE/partition.img
```

Sans -o pour une image qui commence directement par le système de fichiers. Une entrée supprimée listée n’est pas une promesse de contenu récupérable.

## Pièges

- Ne pas mélanger numéro de secteur, numéro d’inode et numéro de bloc.
- Préciser le bon décalage ; une liste vide avec un mauvais offset n’est pas un diagnostic.

## Voir aussi

`mmls`, `icat`, `tsk_recover`, guide 06.
