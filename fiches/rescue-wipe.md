# rescue-wipe — effacer un disque destiné au recyclage

**Couleur : rouge.** Détruit les données du disque choisi ; ce n’est pas une récupération.

**Lancer :** menu SOS, rubrique Effacement ; ou dans un terminal : `rescue-wipe`.

Dans les exemples, remplacer `sdX` et les chemins en majuscules après identification avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. Les outils qui en ont besoin demandent automatiquement les droits sudo.

## Usages

### 1. Lire les options avant de commencer — vert

```bash
rescue-wipe --help
```

Affiche l’aide de la commande sans agir sur un disque.

### 2. Effacer un disque entier vérifié — rouge

```bash
lsblk -o NAME,SIZE,MODEL,SERIAL
rescue-rw /dev/sdX
rescue-wipe /dev/sdX
```

Écrit des zéros sur tout `/dev/sdX`, puis relit entièrement ; choisir le disque à recycler par modèle, taille et série, jamais la source ni une destination contenant encore une copie utile. Retaper les trois valeurs demandées ; le rapport est enregistré hors du disque effacé.

### 3. Renoncer avant l’effacement — rouge

```bash
rescue-wipe /dev/sdX
```

Vise tout `/dev/sdX` : contrôler modèle et série avant l’appel, et ne jamais ouvrir l’original avec `rescue-rw`. Si une confirmation apparaît, une réponse vide annule ; aucune valeur ne doit être retapée en cas de doute.

## Pièges

- Support de démarrage, partition, disque monté ou volume ouvert : refusés. Ne pas contourner les refus.
- Sur SSD, NVMe et mémoire flash, l’écriture de zéros n’atteint pas toutes les cellules ; suivre les méthodes du contrôleur du guide 11.

## Voir aussi

`rescue-rw`, `rescue-ro`, guide 11.
