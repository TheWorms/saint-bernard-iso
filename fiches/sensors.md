# sensors — lire températures et tensions

**Couleur : vert.** Lecture des capteurs déjà reconnus ; ne configure aucun pilote.

**Lancer :** menu SOS, rubrique Matériel et système ; fenêtre `assistant-sensors` ; terminal : `sensors`.

Identifier les disques avec `lsblk -o NAME,SIZE,MODEL,SERIAL` avant de remplacer `sdX`, `sdY` ou `nvme0`. Les lectures intensives se font sur une copie ou un support sain. Ne jamais ouvrir l’original à récupérer avec `rescue-rw`.

## Usages

### 1. Lire les valeurs courantes — vert

```bash
sensors
```

Comparer valeurs, seuils et contexte de charge ; certaines étiquettes ou unités peuvent dépendre de la carte mère.

### 2. Lire les valeurs brutes nommées — vert

```bash
sensors -u
```

Affiche les sous-fonctions et leurs noms techniques pour comprendre une alerte ; aucune correction n’est appliquée.

### 3. Lire les options disponibles — vert

```bash
sensors --help
```

Lire la syntaxe de cette version avant de sélectionner une puce. Ce n’est pas une détection active de nouveaux capteurs.

## Pièges

- Une valeur absente n’est pas une température nulle.
- Ne pas lancer sensors-detect automatiquement pendant une récupération : sa détection matérielle n’est pas cette simple lecture.

## Voir aussi

`stress-ng`, `rescue-hwinfo`, guide 03.
