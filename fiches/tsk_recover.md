# tsk_recover — extraire les fichiers d’une image

**Couleur : orange.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Récupération de fichiers ; fenêtre `assistant-tsk_recover` ; terminal : `sudo tsk_recover`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est la source protégée ; `sdY` une destination distincte. Pour l’analyse, préférer une copie ; ne jamais ouvrir l’original à récupérer avec `rescue-rw`. Les chemins en majuscules sont à remplacer après vérification.

## Usages

### 1. Extraire les fichiers encore alloués — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
sudo tsk_recover -a -o 2048 /mnt/COPIE/disque.img /mnt/DESTINATION/TRAVAIL/alloues
```

Décalage de partition à relever avec mmls. La destination est une autre unité ; -a sélectionne les fichiers encore présents.

### 2. Rechercher les seuls fichiers supprimés — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
sudo tsk_recover /mnt/COPIE/partition.img /mnt/DESTINATION/TRAVAIL/supprimes
```

Sans -a ni -e, cherche les entrées non allouées. L’image de partition commence au système de fichiers, donc sans offset dans cet exemple.

### 3. Extraire toutes les entrées reconnues — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
sudo tsk_recover -e -o 2048 /mnt/COPIE/disque.img /mnt/DESTINATION/TRAVAIL/tout
```

Inclut fichiers alloués et non alloués ; prévoir la place et distinguer fichiers récupérés et fichiers encore intacts.

## Pièges

- Aucune extraction ne doit écrire sur le volume analysé.
- Vérifier contenu et arborescence ; les fichiers fragmentés ou réécrits peuvent être incomplets.

## Voir aussi

`fls`, `mmls`, guide 06.
