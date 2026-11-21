# ntfsfix — diagnostiquer les défauts NTFS élémentaires

**Couleur : rouge.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Systèmes de fichiers ; fenêtre `assistant-ntfsfix` ; terminal : `sudo ntfsfix`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une copie de travail distincte, démontée et sacrifiable. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. Les fichiers de `/tmp` sont en mémoire et disparaissent à l’arrêt.

## Usages

### 1. Simuler les corrections sans écriture — vert

```bash
sudo ntfsfix -n /dev/sdX1
```

Partition NTFS démontée ; -n ne change ni journal ni drapeau.

### 2. Corriger les défauts élémentaires d’une copie — rouge

```bash
rescue-rw /dev/sdY &&
sudo ntfsfix /dev/sdY1
```

Copie démontée : peut corriger MFT/MFTMirr, réinitialiser le journal et demander un contrôle Windows. Sauver les données avant chkdsk.

### 3. Retirer la liste de mauvais secteurs après clonage — rouge

```bash
rescue-rw /dev/sdY &&
sudo ntfsfix -b /dev/sdY1
```

Seulement sur un clone démonté placé sur un nouveau support sain ; ne pas effacer la liste du support défectueux. L’essai vérifie la commande sur une liste vide.

## Pièges

- ntfsfix ne remplace pas chkdsk Windows et ne répare qu’un petit nombre d’incohérences.
- Ne pas effacer le drapeau dirty pour forcer un montage ; laisser Windows contrôler le volume après copie des données.

## Voir aussi

`rescue-ro`, `rescue-rw`, `ddrescue`, guide 09.
