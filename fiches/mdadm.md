# mdadm — lire les membres et assembler un RAID en lecture seule

**Couleur : vert.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Partitions et volumes ; fenêtre `assistant-mdadm` ; terminal : `sudo mdadm`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une copie de travail distincte, démontée et sacrifiable. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. Les fichiers de `/tmp` sont en mémoire et disparaissent à l’arrêt.

## Usages

### 1. Lire les métadonnées d’un membre — vert

```bash
sudo mdadm --examine /dev/sdX1
```

Ne lance pas le RAID. Examiner chaque membre séparément et comparer UUID et compteurs.

### 2. Décrire un RAID déjà assemblé — vert

```bash
sudo mdadm --detail /dev/md/recup
```

Choisir le nom affiché par l’inventaire ; cette lecture ne reconstruit rien.

### 3. Assembler explicitement en lecture seule — vert

```bash
sudo mdadm --assemble --readonly /dev/md/recup /dev/sdX1 /dev/sdZ1
```

Membres cohérents identifiés, non montés ; aucun rescue-rw requis. Après lecture, démonter les systèmes de fichiers puis sudo mdadm --stop /dev/md/recup.

## Pièges

- Ne pas utiliser --create pour récupérer un RAID existant ; noter UUID et ordre des membres.
- Ne pas forcer un assemblage incomplet ni lancer une reconstruction sur les originaux.

## Voir aussi

`rescue-ro`, `rescue-rw`, `lsblk`, guide 08.
