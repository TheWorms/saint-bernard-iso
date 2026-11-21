# rescue-clone — cloner avant de travailler

**Couleur : orange.** Écrit sur une destination ; la source reste protégée.

**Lancer :** menu SOS, rubrique Clonage et images ; ou dans un terminal : `rescue-clone`.

Dans les exemples, remplacer `sdX` et les chemins en majuscules après identification avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. Les outils qui en ont besoin demandent automatiquement les droits sudo.

## Usages

### 1. Créer une image avec son mapfile — orange

```bash
rescue-clone /dev/sdX /mnt/DESTINATION/disque.img --mapfile /mnt/DESTINATION/disque.map
```

Écrit l’image et le mapfile sur la destination montée après `rescue-rw`, jamais sur `/dev/sdX`. Contrôler modèle et série avec `lsblk -o NAME,SIZE,MODEL,SERIAL`, puis `findmnt /mnt/DESTINATION` ; garder les deux fichiers ensemble pour reprendre.

### 2. Alléger la première passe d’un disque instable — orange

```bash
rescue-clone /dev/sdX /mnt/DESTINATION/disque.img --mapfile /mnt/DESTINATION/disque.map --tres-instable --sans-empreinte
```

Écrit les mêmes fichiers sur l’autre disque sain ; vérifier modèle, série et montage de destination avant de lancer. La première passe évite la délimitation, mais les phases suivantes restent proposées : Ctrl+C pour s’arrêter, puis reprendre avec le même mapfile.

### 3. Reprendre le même sauvetage — orange

```bash
rescue-clone /dev/sdX /mnt/DESTINATION/disque.img --mapfile /mnt/DESTINATION/disque.map --inverse
```

Écrit dans l’image et le mapfile existants, sur le disque de destination identifié par modèle et série ; relire `findmnt /mnt/DESTINATION` après chaque rebranchement. Le numéro de série de la source est contrôlé à la reprise ; `--inverse` lit à rebours sans recréer un autre sauvetage.

## Pièges

- Une destination disque entier serait écrasée : préférer l’image ; le disque cible doit être ouvert, démonté et confirmé.
- Le mapfile doit survivre à l’extinction. L’absence d’empreinte ne supprime pas le contrôle d’identité à la reprise.

## Voir aussi

`rescue-rw`, `rescue-mount`, `rescue-recover`, guide 04.
