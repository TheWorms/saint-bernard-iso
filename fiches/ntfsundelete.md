# ntfsundelete — lire et extraire des entrées NTFS supprimées

**Couleur : orange.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Récupération de fichiers ; fenêtre `assistant-ntfsundelete` ; terminal : `sudo ntfsundelete`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est la source protégée ; `sdY` une destination distincte. Pour l’analyse, préférer une copie ; ne jamais ouvrir l’original à récupérer avec `rescue-rw`. Les chemins en majuscules sont à remplacer après vérification.

## Usages

### 1. Scanner les entrées supprimées — vert

```bash
sudo ntfsundelete --scan /dev/sdX1
```

Sur une partition NTFS démontée ou sa copie. L’outil ne modifie pas ce NTFS ; relever inode, nom et pourcentage annoncé.

### 2. Limiter la liste aux entrées annoncées complètes — vert

```bash
sudo ntfsundelete --scan --percentage 100 /dev/sdX1
```

100 % est une estimation fondée sur les métadonnées, pas une garantie que le contenu n’a pas été remplacé.

### 3. Extraire l’inode choisi sur la destination — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
mkdir /mnt/DESTINATION/TRAVAIL/recup &&
sudo ntfsundelete --undelete --inodes 42 --destination /mnt/DESTINATION/TRAVAIL/recup /dev/sdX1
```

Remplacer 42 par l’inode identifié à l’étape de scan et préparer le dossier recup vide. Les fichiers vont sur sdY, jamais sur le NTFS analysé.

## Pièges

- TRIM, réécriture, compression ou chiffrement peuvent empêcher la récupération.
- Contrôler le contenu récupéré : la taille et le nom ne suffisent pas.

## Voir aussi

`ntfsclone`, `photorec`, guide 06.
