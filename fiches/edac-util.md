# edac-util — lire les compteurs ECC du noyau

**Couleur : vert.** Lecture de compteurs ; nécessite des contrôleurs et pilotes EDAC compatibles.

**Lancer :** menu SOS, rubrique Mémoire (RAM) ; fenêtre `assistant-edac-util` ; terminal : `edac-util`.

Identifier les disques avec `lsblk -o NAME,SIZE,MODEL,SERIAL` avant de remplacer `sdX`, `sdY` ou `nvme0`. Les lectures intensives se font sur une copie ou un support sain. Ne jamais ouvrir l’original à récupérer avec `rescue-rw`.

## Usages

### 1. Lister les contrôleurs reconnus — vert

```bash
edac-util -s -v
```

Une absence de contrôleur dans le live ne prouve pas l’absence d’ECC ; vérifier matériel et pilote.

### 2. Lire erreurs corrigées et non corrigées — vert

```bash
edac-util -v
```

Comparer CE et UE avec les symptômes et les étiquettes DIMM déclarées. Aucun compteur n’est remis à zéro par cette lecture.

### 3. Lire les types de rapports disponibles — vert

```bash
edac-util --help
```

Retrouver status et report dans la version installée ; ne pas confondre une sortie sans erreur avec un diagnostic de toute la RAM.

## Pièges

- Une erreur corrigée est un indice à suivre, pas une preuve que le système est désormais sain.
- L’absence de compteurs disponibles doit être déclarée comme telle.

## Voir aussi

`memtester`, `dmidecode`, guide 02.
