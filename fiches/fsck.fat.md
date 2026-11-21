# fsck.fat — contrôler et réparer FAT sur une copie

**Couleur : rouge.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Systèmes de fichiers ; fenêtre `assistant-fsck.fat` ; terminal : `sudo fsck.fat`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une copie de travail distincte, démontée et sacrifiable. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. Les fichiers de `/tmp` sont en mémoire et disparaissent à l’arrêt.

## Usages

### 1. Contrôler FAT sans écrire — vert

```bash
sudo fsck.fat -n /dev/sdX1
```

Aucune réparation ; conserver les erreurs et l’état de la copie.

### 2. Réparer automatiquement une copie — rouge

```bash
rescue-rw /dev/sdY &&
sudo fsck.fat -a /dev/sdY1
```

Copie démontée et sauvegardée ; -a choisit les réparations sans dialogue, ce qui reste une écriture risquée.

### 3. Lister les fichiers pendant le contrôle — vert

```bash
sudo fsck.fat -n -l /dev/sdX1
```

Associe les erreurs aux chemins, sans modifier la FAT.

## Pièges

- FAT12/16/32 seulement, pas exFAT ; démonter avant contrôle.
- Une réparation peut tronquer ou déplacer des chaînes ; sauver d’abord les fichiers lisibles.

## Voir aussi

`rescue-ro`, `rescue-rw`, `ddrescue`, guide 09.
