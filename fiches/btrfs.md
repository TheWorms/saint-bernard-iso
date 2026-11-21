# btrfs — contrôler et extraire sans réparer

**Couleur : rouge.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Systèmes de fichiers ; fenêtre `assistant-btrfs` ; terminal : `sudo btrfs`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une copie de travail distincte, démontée et sacrifiable. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. Les fichiers de `/tmp` sont en mémoire et disparaissent à l’arrêt.

## Usages

### 1. Contrôler la structure en lecture seule — vert

```bash
sudo btrfs check --readonly /dev/sdX1
```

Volume démonté, de préférence une copie ; pas de --repair.

### 2. Simuler une extraction — vert

```bash
sudo btrfs restore -D -v /dev/sdX1 /tmp/apercu-btrfs
```

Simulation sans créer les fichiers ; /tmp reste en mémoire. Selon la version, la liste peut être limitée : seul un essai d’extraction confirme le contenu.

### 3. Extraire vers une destination distincte — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
sudo btrfs restore -v /dev/sdX1 /mnt/DESTINATION/TRAVAIL
```

La source reste démontée et protégée ; choisir un dossier de sortie vide, sans -i pour masquer les erreurs.

## Pièges

- Ne jamais lancer check --repair par réflexe ; cette option peut aggraver la perte.
- Un check ne remplace pas la récupération ; restore écrit des fichiers sur une destination distincte et ne monte pas la source.

## Voir aussi

`rescue-ro`, `rescue-rw`, `ddrescue`, guide 09.
