# rescue-smart — lire la santé d’un disque

**Couleur : vert.** Lit les métadonnées SMART ; les autotests sont jaunes.

**Lancer :** menu SOS, rubrique Diagnostic des disques ; ou dans un terminal : `rescue-smart`.

Dans les exemples, remplacer `sdX` et les chemins en majuscules après identification avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. Les outils qui en ont besoin demandent automatiquement les droits sudo.

## Usages

### 1. Lire le rapport — vert

```bash
rescue-smart /dev/sdX
```

Identifier le disque par modèle et série avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. L’accès derrière un pont USB est recherché automatiquement.

### 2. Obtenir le verdict court — vert

```bash
rescue-smart --verdict /dev/sdX
```

Renvoie `ok`, `surveiller`, `critique` ou `indisponible`, avec les raisons. Un résultat indisponible n’est pas un certificat de bonne santé.

### 3. Lancer un autotest court sur un disque stable — jaune

```bash
rescue-smart --test court /dev/sdX
```

Retaper le nom après vérification du modèle et de la série. Lance le test dans le contrôleur, sans attendre sa fin ; ne jamais le faire avant le clonage d’un disque fragile.

### 4. Lire les options avant de commencer — vert

```bash
rescue-smart --help
```

Affiche l’aide de la commande sans agir sur un disque.

## Pièges

- La lecture seule n’empêche pas un autotest interne : il sollicite le disque.
- Relire le rapport après le délai annoncé ; aucun verdict ne garantit la récupération.

## Voir aussi

`rescue-disks`, `rescue-bench`, `rescue-clone`, guide 01.
