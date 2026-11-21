# foremost — extraire des fichiers par signatures

**Couleur : orange.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Récupération de fichiers ; fenêtre `assistant-foremost` ; terminal : `sudo foremost`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est la source protégée ; `sdY` une destination distincte. Pour l’analyse, préférer une copie ; ne jamais ouvrir l’original à récupérer avec `rescue-rw`. Les chemins en majuscules sont à remplacer après vérification.

## Usages

### 1. Extraire JPEG et PNG dans un dossier neuf — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
sudo foremost -t jpg,png -i /mnt/COPIE/disque.img -o /mnt/DESTINATION/TRAVAIL/photos
```

La destination doit être neuve ; lire aussi audit.txt et comparer les fichiers récupérés à leurs formats attendus.

### 2. Accélérer une recherche alignée sur les secteurs — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
sudo foremost -q -t png -i /mnt/COPIE/disque.img -o /mnt/DESTINATION/TRAVAIL/rapide
```

Le mode rapide ne cherche qu’au début des secteurs : il manque notamment des fichiers imbriqués ou résidents NTFS. Ne pas l’employer comme recherche exhaustive.

### 3. Commencer à un décalage connu — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
sudo foremost -s 2048 -t png -i /mnt/COPIE/disque.img -o /mnt/DESTINATION/TRAVAIL/apres-decalage
```

2048 blocs de 512 octets par défaut : remplacer par le décalage établi, sans confondre octets et secteurs.

## Pièges

- Une récupération par signature perd souvent noms, dates et fragmentation.
- Ne pas utiliser le mode rapide pour conclure qu’un fichier n’existe plus.

## Voir aussi

`photorec`, `mmls`, guide 06.
