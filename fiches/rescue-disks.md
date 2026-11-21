# rescue-disks — identifier les disques

**Couleur : vert.** Inventaire et verdict SMART, sans modification des données.

**Lancer :** menu SOS, rubrique Diagnostic des disques ; ou dans un terminal : `rescue-disks`.

Dans les exemples, remplacer `sdX` et les chemins en majuscules après identification avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. Les outils qui en ont besoin demandent automatiquement les droits sudo.

## Usages

### 1. Faire l’inventaire complet — vert

```bash
rescue-disks
```

Relever modèle, série, taille, bus et état RO/RW avant de choisir une source ou une destination. Le support de démarrage est signalé.

### 2. Éviter les interrogations SMART — vert

```bash
rescue-disks --sans-smart
```

À préférer sur un disque qui se déconnecte : consulte `/sys` et `lsblk`, sans interroger SMART.

### 3. Lire les options avant de commencer — vert

```bash
rescue-disks --help
```

Affiche l’aide de la commande sans agir sur un disque.

## Pièges

- RO/RW décrit l’état du noyau ; un verdict SMART OK n’exclut pas une panne.
- Si bruits ou déconnexions : cloner avant tout test intensif.

## Voir aussi

`rescue-smart`, `rescue-clone`, guide 01.
