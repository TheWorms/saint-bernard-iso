# mc — parcourir et copier avec deux panneaux

**Couleur : aucun.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Bureau ; fenêtre `assistant-mc` ; terminal : `mc`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une cible distincte, sacrifiable pour les effacements. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. `/tmp` et les rapports du live sont en RAM, perdus à l’arrêt. Un serveur distant doit être autorisé et son identité vérifiée.

## Usages

### 1. Parcourir une copie protégée — vert

```bash
mc /mnt/COPIE /tmp
```

Tab change de panneau, F3 lit un fichier, F10 quitte. La source reste protégée.

### 2. Copier vers une destination ouverte — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
mc /mnt/COPIE /mnt/DESTINATION/TRAVAIL
```

Choisir le fichier, F5 puis relire la cible ; comparer ensuite contenu et taille. Ne pas utiliser F6 sur la source.

### 3. Lire un rapport dans le visualiseur — vert

```bash
mc --view /tmp/rapport.txt
```

Fichier texte existant ; F10 quitte le visualiseur sans modifier le rapport.

## Pièges

- F5 copie, F6 déplace, F8 supprime : relire l’action et le panneau cible. Ne pas déplacer les originaux.
- Un lancement réussi ne prouve pas une copie ; vérifier les fichiers transférés. Ne pas ouvrir le gestionnaire en root par habitude.

## Voir aussi

`rescue-ro`, `rescue-rw`, `sha256sum`, guide 13.
