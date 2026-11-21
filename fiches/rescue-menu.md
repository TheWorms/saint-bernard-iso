# rescue-menu — ouvrir le menu texte de secours

**Couleur : vert.** Le menu laisse chaque commande appliquer ses propres garde-fous.

**Lancer :** menu SOS, rubrique Bureau ; ou dans un terminal : `rescue-menu`.

Dans les exemples, remplacer `sdX` et les chemins en majuscules après identification avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. Les outils qui en ont besoin demandent automatiquement les droits sudo.

## Usages

### 1. Ouvrir le menu texte — vert

```bash
rescue-menu
```

Naviguer au clavier ; Échap ou Quitter rend l’invite. Les actions orange ou rouges restent des opérations à confirmer sur la bonne destination.

### 2. Lister les entrées sans ouvrir le menu — vert

```bash
rescue-menu --lister
```

Affiche une entrée par ligne, utile depuis une console non interactive. Ne lance aucun outil.

### 3. Lire les options avant de commencer — vert

```bash
rescue-menu --help
```

Affiche l’aide de la commande sans agir sur un disque.

## Pièges

- Le menu de secours texte n’est pas le menu SOS graphique ; les intitulés peuvent différer.
- Choisir une action d’écriture ne dispense ni de `rescue-rw` ni des confirmations de l’outil.

## Voir aussi

`rescue-help`, `rescue-disks`, guide 13.
