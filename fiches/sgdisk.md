# sgdisk — examiner et écrire une GPT

**Couleur : rouge.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Partitions et volumes ; fenêtre `assistant-sgdisk` ; terminal : `sudo sgdisk`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une copie de travail distincte, démontée et sacrifiable. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. Les fichiers de `/tmp` sont en mémoire et disparaissent à l’arrêt.

## Usages

### 1. Afficher la GPT — vert

```bash
sudo sgdisk --print /dev/sdX
```

Lecture des numéros, limites et types ; aucune écriture.

### 2. Vérifier les deux tables et leurs sommes de contrôle — vert

```bash
sudo sgdisk --verify /dev/sdX
```

Signale les incohérences, sans les réparer. Une sauvegarde valide reste nécessaire.

### 3. Ajouter une partition Linux à une copie GPT — rouge

```bash
rescue-rw /dev/sdY &&
sudo sgdisk --new=2:0:+8M --typecode=2:8300 --change-name=2:TRAVAIL /dev/sdY
```

La partition 2 doit être libre et la copie démontée ; la taille de 8 Mio est un exemple.

## Pièges

- Les options de création écrivent immédiatement : pas de menu de confirmation.
- Une vérification GPT ne contrôle pas les systèmes de fichiers ; conserver une sauvegarde de table.

## Voir aussi

`rescue-ro`, `rescue-rw`, `lsblk`, guide 08.
