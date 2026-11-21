# rclone — copier vers un stockage configuré

**Couleur : orange.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Sauvegarde ; fenêtre `assistant-rclone` ; terminal : `rclone`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une cible distincte, sacrifiable pour les effacements. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. `/tmp` et les rapports du live sont en RAM, perdus à l’arrêt. Un serveur distant doit être autorisé et son identité vérifiée.

## Usages

### 1. Simuler une copie distante — vert

```bash
rclone copy --dry-run /mnt/COPIE/recuperation homelab:intervention/recup
```

homelab est un distant déjà configuré et autorisé. La simulation ne valide ni le transfert réel ni la capacité restante.

### 2. Copier sans supprimer le distant — orange

```bash
rclone copy -P /mnt/COPIE/recuperation homelab:intervention/recup
```

Écrit sur le distant autorisé, pas sur la source. Choisir un dossier propre à l’intervention.

### 3. Comparer source et distant — vert

```bash
rclone check --one-way /mnt/COPIE/recuperation homelab:intervention/recup
```

--one-way autorise des fichiers supplémentaires à destination ; ne les efface pas. Si le distant n’offre pas de somme compatible, utiliser --download pour relire.

## Pièges

- copy conserve les fichiers supplémentaires du destinataire ; sync peut les effacer.
- Configurer soi-même le distant et vérifier son identité. La configuration peut contenir des secrets ; ne pas l’inclure dans les rapports.

## Voir aussi

`rescue-ro`, `rescue-rw`, `sha256sum`, guide 12.
