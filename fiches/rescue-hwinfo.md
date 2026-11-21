# rescue-hwinfo — relever le matériel

**Couleur : vert.** Lit le matériel et enregistre un relevé hors des disques traités.

**Lancer :** menu SOS, rubrique Matériel et système ; ou dans un terminal : `rescue-hwinfo`.

Dans les exemples, remplacer `sdX` et les chemins en majuscules après identification avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. Les outils qui en ont besoin demandent automatiquement les droits sudo.

## Usages

### 1. Lire le résumé et les relevés — vert

```bash
rescue-hwinfo
```

Affiche CPU, mémoire, contrôleurs, pilotes et erreurs du noyau. Le chemin de sauvegarde indique si le relevé est durable ou seulement en mémoire.

### 2. Obtenir le chemin du fichier — vert

```bash
rescue-hwinfo --fichier
```

Produit le relevé mais affiche seulement son chemin, utile pour le retrouver sans recopier tout le terminal.

### 3. Lire les options avant de commencer — vert

```bash
rescue-hwinfo --help
```

Affiche l’aide de la commande sans agir sur un disque.

## Pièges

- Sans `RESCUE-DATA`, le fichier est perdu à l’extinction.
- Les relevés contiennent des identifiants matériels : relire avant de partager.

## Voir aussi

`rescue-collect`, `rescue-disks`, guide 03.
