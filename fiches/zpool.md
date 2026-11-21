# zpool — découvrir et importer ZFS en lecture seule

**Couleur : vert.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Partitions et volumes ; fenêtre `assistant-zpool` ; terminal : `sudo zpool`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une copie de travail distincte, démontée et sacrifiable. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. Les fichiers de `/tmp` sont en mémoire et disparaissent à l’arrêt.

## Usages

### 1. Lister les pools importables — vert

```bash
sudo zpool import
```

Sans nom, ne fait que découvrir. Noter nom, identifiant, membres et avertissements.

### 2. Importer sans montage et en lecture seule — vert

```bash
sudo zpool import -N -o readonly=on -R /mnt/zfs POOL
```

Remplacer POOL par le nom confirmé. Ne pas forcer un pool possiblement actif ; exporter avec sudo zpool export POOL après lecture.

### 3. Lire l’état détaillé d’un pool importé RO — vert

```bash
sudo zpool status -v POOL
```

État et erreurs connus ; aucune vérification intégrale ni réparation n’est lancée.

## Pièges

- readonly=on doit être demandé à l’import ; -N évite les montages automatiques.
- Ne pas employer create, destroy, scrub ou clear sur les originaux. N’ajouter -f qu’après avoir exclu un pool encore actif ailleurs.

## Voir aussi

`rescue-ro`, `rescue-rw`, `lsblk`, guide 08.
