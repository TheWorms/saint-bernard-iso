# fdisk — lister ou éditer une table MBR/GPT

**Couleur : rouge.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Partitions et volumes ; fenêtre `assistant-fdisk` ; terminal : `sudo fdisk`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une copie de travail distincte, démontée et sacrifiable. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. Les fichiers de `/tmp` sont en mémoire et disparaissent à l’arrêt.

## Usages

### 1. Lister les partitions — vert

```bash
sudo fdisk --list /dev/sdX
```

Lecture seule des limites et types, sur la source protégée ou sa copie.

### 2. Ajouter une partition sur une copie MBR — rouge

```bash
rescue-rw /dev/sdY &&
sudo fdisk /dev/sdY
```

Copie démontée : n, primaire p, numéro libre, début et fin ; p pour relire, w pour écrire. L’essai utilise une table MBR connue, pas les réponses d’un disque réel.

### 3. Afficher des colonnes explicites en secteurs — vert

```bash
sudo fdisk --list --output Device,Start,End,Sectors,Size,Type /dev/sdX
```

Utile pour comparer deux inventaires sans dépendre des colonnes par défaut.

## Pièges

- w écrit la table ; q abandonne. Le dialogue dépend de la table existante.
- Ne pas déplacer les débuts des partitions pour résoudre un simple problème de montage.

## Voir aussi

`rescue-ro`, `rescue-rw`, `lsblk`, guide 08.
