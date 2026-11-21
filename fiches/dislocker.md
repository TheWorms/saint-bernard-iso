# dislocker — lire un volume BitLocker

**Couleur : vert.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Partitions et volumes ; fenêtre `assistant-dislocker` ; terminal : `sudo dislocker`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une copie de travail distincte, démontée et sacrifiable. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. Les fichiers de `/tmp` sont en mémoire et disparaissent à l’arrêt.

## Usages

### 1. Lire les métadonnées BitLocker — vert

```bash
sudo dislocker-metadata -V /dev/sdX1
```

Ce compagnon ne déchiffre pas les fichiers ; vérifier que la partition est bien BitLocker.

### 2. Exposer le fichier déchiffré sans écriture — vert

```bash
sudo mkdir -p /mnt/DECHIFFRE &&
sudo dislocker -r -V /dev/sdX1 -u -- /mnt/DECHIFFRE
```

Le mot de passe est demandé au terminal. Utiliser un dossier vide dédié, puis vérifier dislocker-file ; le montage FUSE doit rester vivant.

### 3. Monter le NTFS déchiffré en lecture seule — vert

```bash
sudo mkdir -p /mnt/LECTURE &&
sudo mount -o loop,ro /mnt/DECHIFFRE/dislocker-file /mnt/LECTURE
```

Après l’ouverture -r ci-dessus. Pour finir : sudo umount /mnt/LECTURE puis sudo umount /mnt/DECHIFFRE ; ne jamais inverser cet ordre.

## Pièges

- Le lecteur doit rester protégé ; -r interdit l’écriture par dislocker et le montage NTFS doit rester ro.
- Ne jamais écrire la clé de récupération ou le mot de passe réel dans la ligne de commande ni les captures.

## Voir aussi

`rescue-ro`, `rescue-rw`, `lsblk`, guide 08.
