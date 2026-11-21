# dd — copier des octets sans reprise

**Couleur : orange.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Clonage et images ; fenêtre `assistant-dd` ; terminal : `sudo dd`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est la source protégée ; `sdY` une destination distincte. Pour l’analyse, préférer une copie ; ne jamais ouvrir l’original à récupérer avec `rescue-rw`. Les chemins en majuscules sont à remplacer après vérification.

## Usages

### 1. Créer une image neuve d’un disque sain — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
sudo dd if=/dev/sdX of=/mnt/DESTINATION/TRAVAIL/disque-neuf.img bs=4M iflag=fullblock conv=excl,fsync status=progress
```

Source saine ou copie stable seulement. conv=excl refuse un fichier déjà présent ; dd ne remplace pas ddrescue pour un disque défaillant.

### 2. Restaurer une copie sur un disque sacrifiable — rouge

```bash
rescue-rw /dev/sdY &&
sudo dd if=/mnt/COPIE/disque.img of=/dev/sdY bs=4M iflag=fullblock conv=fsync status=progress
```

Écrase le début de sdY sur toute la taille de l’image. Vérifier modèle, série et capacité ; la source de récupération reste protégée.

### 3. Extraire le premier secteur dans le live — vert

```bash
sudo dd if=/dev/sdX of=/tmp/secteur.bin bs=512 count=1 status=none
```

Lit 512 octets et écrit uniquement dans /tmp en RAM. Ce fichier n’est pas une sauvegarde suffisante d’une table GPT.

## Pièges

- excl est une conversion : conv=excl,fsync refuse un fichier existant et synchronise la sortie ; oflag ne possède pas de valeur excl.
- if lit et of écrit ; inverser les deux détruit la mauvaise cible.
- Sans carte de reprise, les erreurs et interruptions ne se gèrent pas comme avec ddrescue.

## Voir aussi

`ddrescue`, `sha256sum`, guide 04.
