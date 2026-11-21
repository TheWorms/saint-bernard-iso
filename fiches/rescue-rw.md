# rescue-rw — autoriser l’écriture sur une destination

**Couleur : orange.** Autorise les programmes à modifier le disque choisi, sans copier lui-même de données.

**Lancer :** menu SOS, rubrique Partitions et volumes ; ou dans un terminal : `rescue-rw`.

Dans les exemples, remplacer `sdX` et les chemins en majuscules après identification avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. Les outils qui en ont besoin demandent automatiquement les droits sudo.

## Usages

### 1. Ouvrir une destination saine — orange

```bash
lsblk -o NAME,SIZE,MODEL,SERIAL
rescue-rw /dev/sdX
```

L’écriture devient possible sur tout `/dev/sdX` et ses partitions. Vérifier modèle, série et taille, puis retaper le nom demandé ; jamais le disque source à récupérer.

### 2. Renoncer en cas de doute — orange

```bash
rescue-rw /dev/sdX
```

La cible proposée est `/dev/sdX` : contrôler son modèle et sa série, puis appuyer sur Entrée sans rien retaper pour renoncer. Ne jamais confirmer une source ; une confirmation correcte autoriserait tous les programmes à l’écrire.

### 3. Refermer après intervention — vert

```bash
rescue-ro /dev/sdX
```

Après démontage, referme l’autorisation. Contrôler le même modèle et numéro de série : le nom peut changer après débranchement.

## Pièges

- Donner un disque entier, pas une partition ; le support de démarrage est refusé.
- L’autorisation reste active jusqu’à `rescue-ro`, au débranchement ou à l’extinction.

## Voir aussi

`rescue-ro`, `rescue-mount`, guide 08.
