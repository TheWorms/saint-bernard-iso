# photorec — récupérer par signatures vers un autre support

**Couleur : orange.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Récupération de fichiers ; fenêtre `assistant-photorec` ; terminal : `sudo photorec`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est la source protégée ; `sdY` une destination distincte. Pour l’analyse, préférer une copie ; ne jamais ouvrir l’original à récupérer avec `rescue-rw`. Les chemins en majuscules sont à remplacer après vérification.

## Usages

### 1. Choisir les formats et la destination au clavier — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
cd /tmp &&
sudo photorec /log /d /mnt/DESTINATION/TRAVAIL/recup /mnt/COPIE/disque.img
```

Lire l’image ou une copie protégée. Choisir File Opt puis une destination distincte ; les noms et arborescences d’origine ne sont généralement pas conservés.

### 2. Rechercher seulement les PNG sans dialogue — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
cd /tmp &&
sudo photorec /d /mnt/DESTINATION/TRAVAIL/png /cmd /mnt/COPIE/disque.img fileopt,everything,disable,png,enable,search
```

PhotoRec ajoute un numéro au dossier de sortie (par exemple png.1). Écrit les fichiers récupérés dans une destination neuve ; vérifier leur contenu avant restitution. Cette recherche parcourt les données et peut être longue sur une vraie image.

### 3. Reprendre une session interrompue — orange

```bash
rescue-rw /dev/sdY &&
cd /tmp &&
sudo photorec /log /d /mnt/DESTINATION/TRAVAIL/recup /mnt/COPIE/disque.img
```

Retrouver photorec.ses dans le dossier de session et accepter la reprise proposée uniquement pour la même image et la même destination déjà montée.

## Pièges

- Une signature n’est pas un nom de fichier ni une garantie d’intégrité.
- Ne jamais récupérer les fichiers sur le volume d’où ils proviennent.

## Voir aussi

`foremost`, `testdisk`, guide 06.
