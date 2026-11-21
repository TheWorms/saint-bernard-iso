# sfdisk — sauvegarder et restaurer une table

**Couleur : vert.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Partitions et volumes ; fenêtre `assistant-sfdisk` ; terminal : `sudo sfdisk`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une copie de travail distincte, démontée et sacrifiable. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. Les fichiers de `/tmp` sont en mémoire et disparaissent à l’arrêt.

## Usages

### 1. Sauver la table dans le live — vert

```bash
sudo sfdisk --dump /dev/sdX > /tmp/table-sdX.sfdisk
```

Le fichier /tmp est en mémoire et disparaît à l’arrêt ; le copier ensuite dans un rapport conservé.

### 2. Restaurer une table sur une copie sacrifiable — rouge

```bash
rescue-rw /dev/sdY &&
sudo sfdisk /dev/sdY < /tmp/table-sdX.sfdisk
```

sdY est démonté et de géométrie compatible. Relire le dump et ses identifiants avant la restauration.

### 3. Exporter un inventaire JSON — vert

```bash
sudo sfdisk --json /dev/sdX
```

Les tailles et positions sont en secteurs ; garder aussi l’unité et la taille de secteur du document.

## Pièges

- Un dump est du texte, pas une copie des fichiers ni des secteurs d’amorçage.
- La restauration écrit immédiatement : vérifier taille et taille de secteur de la destination, distincte de l’original.

## Voir aussi

`rescue-ro`, `rescue-rw`, `lsblk`, guide 08.
