# rescue-collect — conserver le diagnostic de la machine

**Couleur : vert.** Lit les métadonnées et crée une archive de diagnostic hors des disques traités.

**Lancer :** menu SOS, rubrique Matériel et système ; ou dans un terminal : `rescue-collect`.

Dans les exemples, remplacer `sdX` et les chemins en majuscules après identification avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. Les outils qui en ont besoin demandent automatiquement les droits sudo.

## Usages

### 1. Produire le diagnostic complet — vert

```bash
rescue-collect
```

Enregistre dans `RESCUE-DATA/reports/`, sinon en mémoire. Ne prend aucun fichier utilisateur, mais inclut les numéros de série : conserver l’archive comme sensible.

### 2. Épargner les interrogations SMART — vert

```bash
rescue-collect --sans-smart
```

À utiliser si un disque lâche : évite les requêtes SMART. Les relevés système et des volumes restent inclus.

### 3. Lire les options avant de commencer — vert

```bash
rescue-collect --help
```

Affiche l’aide de la commande sans agir sur un disque.

## Pièges

- Une archive en mémoire disparaît à l’extinction : la copier sur une destination saine.
- Vérifier le contenu et retirer les identifiants avant de transmettre une archive ; elle ne doit pas entrer dans un patch.

## Voir aussi

`rescue-hwinfo`, `rescue-report`, guide 03.
