# debugfs — inspecter ext et extraire un fichier

**Couleur : rouge.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Systèmes de fichiers ; fenêtre `assistant-debugfs` ; terminal : `sudo debugfs`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une copie de travail distincte, démontée et sacrifiable. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. Les fichiers de `/tmp` sont en mémoire et disparaissent à l’arrêt.

## Usages

### 1. Lire les statistiques ext — vert

```bash
sudo debugfs -R 'stats' /dev/sdX1
```

Partition ext démontée, de préférence une copie.

### 2. Lister un répertoire connu — vert

```bash
sudo debugfs -R 'ls -l /Documents' /dev/sdX1
```

Adapter le chemin interne au volume ; ne pas le confondre avec un chemin du live.

### 3. Extraire un fichier vers un disque distinct — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
sudo debugfs -R 'dump /Documents/lettre.txt /mnt/DESTINATION/TRAVAIL/lettre.txt' /dev/sdX1
```

La source reste protégée sans -w ; seule la destination reçoit le fichier. Choisir un nom de sortie inexistant.

## Pièges

- Sans -w, debugfs lit seulement ; -w peut endommager les métadonnées.
- Certaines erreurs de commande ne donnent pas un code de sortie non nul : vérifier le contenu effectivement obtenu.

## Voir aussi

`rescue-ro`, `rescue-rw`, `ddrescue`, guide 09.
