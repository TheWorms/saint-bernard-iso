# extundelete — essayer une récupération ext3 ou ext4 compatible

**Couleur : orange.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Récupération de fichiers ; fenêtre `assistant-extundelete` ; terminal : `sudo extundelete`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est la source protégée ; `sdY` une destination distincte. Pour l’analyse, préférer une copie ; ne jamais ouvrir l’original à récupérer avec `rescue-rw`. Les chemins en majuscules sont à remplacer après vérification.

## Usages

### 1. Lire le superbloc d’une copie — vert

```bash
sudo extundelete /mnt/COPIE/partition.img --superblock
```

L’image représente le système de fichiers lui-même, pas un disque entier avec table. Des fonctionnalités ext4 modernes peuvent être incompatibles.

### 2. Tenter un chemin précis — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
sudo extundelete /mnt/COPIE/partition.img --restore-file Documents/lettre.txt -o /mnt/DESTINATION/TRAVAIL/recup
```

Le chemin est relatif à la racine du système de fichiers. Le journal doit encore contenir les métadonnées utiles ; la destination est distincte.

### 3. Tenter toutes les entrées retrouvées — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
sudo extundelete /mnt/COPIE/partition.img --restore-all -o /mnt/DESTINATION/TRAVAIL/tout
```

Peut prendre longtemps sur une image réelle ; lire les refus et vérifier chaque résultat. Ne jamais monter l’original en écriture pour faciliter l’opération.

## Pièges

- Outil ancien : ne pas lancer de réparation préalable sur l’original pour satisfaire ses exigences.
- Un fichier réécrit ou écarté du journal peut être irrécupérable.

## Voir aussi

`ext4magic`, `tsk_recover`, guide 06.
