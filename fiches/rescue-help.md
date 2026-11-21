# rescue-help — suivre la méthode de récupération

**Couleur : vert.** Affiche un mémo ; ne lance aucune opération sur un disque.

**Lancer :** menu SOS, rubrique Bureau ; ou dans un terminal : `rescue-help`.

Dans les exemples, remplacer `sdX` et les chemins en majuscules après identification avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. Les outils qui en ont besoin demandent automatiquement les droits sudo.

## Usages

### 1. Lire le mémo page par page — vert

```bash
rescue-help
```

Dans un terminal, ouvre `less` : Espace avance et `q` ferme le mémo. Le menu SOS propose aussi les guides complets.

### 2. Afficher le mémo sans pagination — vert

```bash
rescue-help | cat
```

Pratique pour retrouver toute la procédure dans l’historique du terminal. Les commandes citées restent des exemples à adapter.

### 3. Lire les options avant de commencer — vert

```bash
rescue-help --help
```

Affiche l’aide de la commande sans agir sur un disque.

## Pièges

- Lire un exemple ne vérifie pas l’identité des disques ; contrôler modèle, taille et série avant toute écriture.
- Une urgence SMART passe avant les tests de confort : cloner en priorité.

## Voir aussi

`rescue-menu`, `rescue-disks`, guide 00.
