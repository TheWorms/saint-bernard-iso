# ddrescue — cloner avec une carte de reprise

**Couleur : orange.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Clonage et images ; fenêtre `assistant-ddrescue` ; terminal : `sudo ddrescue`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est la source protégée ; `sdY` une destination distincte. Pour l’analyse, préférer une copie ; ne jamais ouvrir l’original à récupérer avec `rescue-rw`. Les chemins en majuscules sont à remplacer après vérification.

## Usages

### 1. Faire la première passe vers une image — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
sudo ddrescue --ask -n /dev/sdX /mnt/DESTINATION/TRAVAIL/disque.img /mnt/DESTINATION/TRAVAIL/disque.map
```

sdX est la source protégée, sdY un autre disque sain. Vérifier les deux identités à la question --ask. Garder image et mapfile ensemble sur la destination.

### 2. Reprendre avec une tentative supplémentaire — orange

```bash
rescue-rw /dev/sdY &&
sudo ddrescue --ask -d -r1 /dev/sdX /mnt/DESTINATION/TRAVAIL/disque.img /mnt/DESTINATION/TRAVAIL/disque.map
```

Reprendre la destination déjà montée et exactement le même couple image/mapfile. Ne pas relancer des centaines de tentatives sur un disque qui se dégrade.

### 3. Cloner vers un disque sacrifiable — rouge

```bash
rescue-rw /dev/sdY &&
sudo ddrescue --ask -f -n /dev/sdX /dev/sdY /mnt/JOURNAUX/disque.map
```

Écrase sdY entier ; sa taille doit être suffisante. JOURNAUX est une destination saine distincte, déjà montée en écriture. Ne jamais inverser source et cible.

## Pièges

- -f autorise une cible bloc : ce n’est pas une réparation.
- La carte de reprise décrit les zones lues, pas l’intégrité logique des fichiers.

## Voir aussi

`ddrescuelog`, `rescue-clone`, guide 04.
