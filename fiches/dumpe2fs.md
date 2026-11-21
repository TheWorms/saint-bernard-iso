# dumpe2fs — lire les métadonnées ext

**Couleur : vert.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Systèmes de fichiers ; fenêtre `assistant-dumpe2fs` ; terminal : `sudo dumpe2fs`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une copie de travail distincte, démontée et sacrifiable. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. Les fichiers de `/tmp` sont en mémoire et disparaissent à l’arrêt.

## Usages

### 1. Lire le résumé du superbloc — vert

```bash
sudo dumpe2fs -h /dev/sdX1
```

Affiche UUID, état et fonctions ext sans écrire.

### 2. Relever les groupes et superblocs de secours — vert

```bash
sudo dumpe2fs /dev/sdX1
```

Sortie longue ; noter les emplacements avant toute tentative avec e2fsck -b sur une copie.

### 3. Lire la liste des blocs marqués défectueux — vert

```bash
sudo dumpe2fs -b /dev/sdX1
```

Lit la liste existante ; ne teste pas le support et n’ajoute aucun bloc.

## Pièges

- Les valeurs d’un système monté peuvent changer pendant la lecture.
- Ne pas déduire qu’un superbloc de secours est utilisable sans comparer géométrie et options.

## Voir aussi

`rescue-ro`, `rescue-rw`, `ddrescue`, guide 09.
