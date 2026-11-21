# rsync — copier puis comparer des fichiers

**Couleur : orange.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Réseau ; fenêtre `assistant-rsync` ; terminal : `rsync`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une cible distincte, sacrifiable pour les effacements. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. `/tmp` et les rapports du live sont en RAM, perdus à l’arrêt. Un serveur distant doit être autorisé et son identité vérifiée.

## Usages

### 1. Simuler la copie — vert

```bash
rsync -a -n -i /mnt/COPIE/recuperation/ /tmp/apercu-rsync/
```

Simulation sans écriture des fichiers ; cible en RAM pour l’exemple.

### 2. Copier avec reprise partielle — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
rsync -a --partial --info=progress2 /mnt/COPIE/recuperation/ /mnt/DESTINATION/TRAVAIL/recuperation/
```

Source montée RO, destination distincte ouverte RW. Pour un distant autorisé, remplacer la cible par UTILISATEUR@SERVEUR:/CHEMIN/.

### 3. Comparer le contenu sans recopier — vert

```bash
rsync -a -n -c -i /mnt/COPIE/recuperation/ /mnt/DESTINATION/TRAVAIL/recuperation/
```

-c relit les fichiers et compare les sommes ; une sortie vide sans erreur indique l’accord pour ce périmètre.

## Pièges

- La barre finale source/ copie son contenu ; sans elle, le dossier lui-même peut être recréé.
- Pas de --delete sur une récupération. -a ne conserve pas à lui seul ACL, attributs étendus et liens physiques ; voir le guide pour -HAX et les droits.

## Voir aussi

`rescue-ro`, `rescue-rw`, `sha256sum`, guide 13.
