# mmls — lire la table de partitions d’une image

**Couleur : vert.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Récupération de fichiers ; fenêtre `assistant-mmls` ; terminal : `sudo mmls`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est la source protégée ; `sdY` une destination distincte. Pour l’analyse, préférer une copie ; ne jamais ouvrir l’original à récupérer avec `rescue-rw`. Les chemins en majuscules sont à remplacer après vérification.

## Usages

### 1. Lire les bornes des partitions — vert

```bash
sudo mmls /mnt/COPIE/disque.img
```

Relever début, fin et unités avant d’appeler fls ou tsk_recover. Ne change pas la table.

### 2. Ajouter les tailles en octets — vert

```bash
sudo mmls -B /mnt/COPIE/disque.img
```

Comparer les unités affichées et les octets ; les secteurs ne valent pas toujours 512 octets sur le matériel réel.

### 3. Préciser une table DOS déjà identifiée — vert

```bash
sudo mmls -t dos /mnt/COPIE/disque.img
```

Seulement si l’image est connue comme DOS/MBR ; ne pas imposer ce type à une GPT pour faire disparaître une erreur.

## Pièges

- Une image de partition seule n’a pas forcément de table.
- Les secteurs indiqués doivent être interprétés avec la taille de secteur appropriée.

## Voir aussi

`fls`, `testdisk`, guide 06.
