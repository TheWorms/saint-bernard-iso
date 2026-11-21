# parted — lire et modifier une table de partitions

**Couleur : rouge.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Partitions et volumes ; fenêtre `assistant-parted` ; terminal : `sudo parted`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une copie de travail distincte, démontée et sacrifiable. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. Les fichiers de `/tmp` sont en mémoire et disparaissent à l’arrêt.

## Usages

### 1. Lire les secteurs et les limites — vert

```bash
sudo parted /dev/sdX unit s print
```

Lecture seule sur une copie ou un support stable ; les unités s désignent des secteurs.

### 2. Créer une table GPT sur une cible vide — rouge

```bash
rescue-rw /dev/sdY &&
sudo parted --script /dev/sdY mklabel gpt
```

Écrase la table de sdY, copie de travail démontée et sacrifiable.

### 3. Ajouter une partition dans un espace libre connu — rouge

```bash
rescue-rw /dev/sdY &&
sudo parted --script /dev/sdY mkpart TRAVAIL ext4 1MiB 9MiB
```

Cible GPT démontée sans partition dans cet intervalle. Indiquer ext4 ne formate rien.

## Pièges

- mklabel détruit la table existante ; mkpart ne crée pas le système de fichiers.
- Ne pas modifier une table sur un disque monté ; sauver sa table avant toute écriture.

## Voir aussi

`rescue-ro`, `rescue-rw`, `lsblk`, guide 08.
