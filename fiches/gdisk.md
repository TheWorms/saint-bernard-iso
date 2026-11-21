# gdisk — examiner ou éditer une GPT avec un dialogue

**Couleur : rouge.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Partitions et volumes ; fenêtre `assistant-gdisk` ; terminal : `sudo gdisk`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une copie de travail distincte, démontée et sacrifiable. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. Les fichiers de `/tmp` sont en mémoire et disparaissent à l’arrêt.

## Usages

### 1. Lister la GPT sans dialogue — vert

```bash
sudo gdisk -l /dev/sdX
```

Lecture seule ; conserver l’avertissement si GPT et MBR se contredisent.

### 2. Créer une partition sur une copie — rouge

```bash
rescue-rw /dev/sdY &&
sudo gdisk /dev/sdY
```

Sur une copie GPT démontée : n, numéro libre, limites choisies, type ; p pour relire, w puis confirmation pour écrire. Ne pas recopier ces réponses sur un disque inconnu.

### 3. Vérifier puis quitter sans écrire — vert

```bash
sudo gdisk /dev/sdX
```

Saisir v pour vérifier puis q pour sortir ; ne pas utiliser w sur la source.

## Pièges

- Le menu travaille en mémoire jusqu’à w ; q quitte sans enregistrer.
- Une conversion MBR/GPT et les propositions de récupération exigent une sauvegarde et une décision humaine.

## Voir aussi

`rescue-ro`, `rescue-rw`, `lsblk`, guide 08.
