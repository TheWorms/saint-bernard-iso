# shred — écraser une cible sacrifiable

**Couleur : rouge.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Effacement ; fenêtre `assistant-shred` ; terminal : `sudo shred`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une cible distincte, sacrifiable pour les effacements. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. `/tmp` et les rapports du live sont en RAM, perdus à l’arrêt. Un serveur distant doit être autorisé et son identité vérifiée.

## Usages

### 1. Écraser puis terminer par des zéros — rouge

```bash
rescue-rw /dev/sdY &&
sudo shred -v -n 1 -z /dev/sdY
```

Écrase la totalité du disque sdY confirmé, après démontage. Une passe aléatoire puis une passe finale de zéros.

### 2. Écraser et supprimer un fichier de travail — rouge

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
sudo shred -u -n 1 -z /mnt/DESTINATION/TRAVAIL/A-EFFACER
```

Fichier sacrifiable à nom vérifié. Ne pas promettre un effacement physique sûr d’un fichier sur ext4 journalisé ou un SSD.

### 3. Remplir seulement de zéros — rouge

```bash
rescue-rw /dev/sdY &&
sudo shred -v -n 0 -z /dev/sdY
```

Écriture totale, sans passe aléatoire. Utile pour une cible de test ; ne constitue pas une commande Secure Erase d’un SSD.

## Pièges

- Pas de garantie sur SSD, snapshots, CoW ou sauvegardes ; un fichier supprimé n’efface pas toutes ses copies.
- Relire if/of ne s’applique pas ici : l’argument est directement la cible détruite. Conserver la preuve d’identité du support.

## Voir aussi

`rescue-ro`, `rescue-rw`, `sha256sum`, guide 11.
