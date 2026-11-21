# rescue-report — produire le rapport d’intervention

**Couleur : vert.** Interroge SMART et rassemble les actions ; ne modifie pas le disque traité.

**Lancer :** menu SOS, rubrique Diagnostic des disques ; ou dans un terminal : `rescue-report`.

Dans les exemples, remplacer `sdX` et les chemins en majuscules après identification avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. Les outils qui en ont besoin demandent automatiquement les droits sudo.

## Usages

### 1. Créer le rapport d’un disque — vert

```bash
rescue-report /dev/sdX
```

Vérifier modèle et série ; répondre aux questions ou passer avec Entrée. Le HTML est conservé dans `RESCUE-DATA/reports/`, sinon en mémoire.

### 2. Joindre les résultats du clonage — vert

```bash
rescue-report /dev/sdX --image /mnt/DESTINATION/disque.img --mapfile /mnt/DESTINATION/disque.map
```

Lit les informations de l’image et du mapfile ; indique volume récupéré, durée et empreinte si disponibles dans les journaux. Utiliser les fichiers du même sauvetage.

### 3. Ajouter le bilan des fichiers retrouvés — vert

```bash
rescue-report /dev/sdX --recup /mnt/DESTINATION/fichiers
```

Compte les fichiers et leur volume par type, sans inclure leurs noms dans le rapport. Vérifier que le dossier correspond bien à cette intervention.

## Pièges

- Sans `RESCUE-DATA`, exporter le rapport avant l’extinction.
- Le rapport contient des identifiants et les réponses saisies : ne pas le publier ni l’ajouter aux patchs. Aucune garantie de récupération.

## Voir aussi

`rescue-collect`, `rescue-clone`, guide 01.
