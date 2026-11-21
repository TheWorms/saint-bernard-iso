# xfs_repair — vérifier ou réparer XFS démonté

**Couleur : rouge.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Systèmes de fichiers ; fenêtre `assistant-xfs_repair` ; terminal : `sudo xfs_repair`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une copie de travail distincte, démontée et sacrifiable. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. Les fichiers de `/tmp` sont en mémoire et disparaissent à l’arrêt.

## Usages

### 1. Simuler un contrôle sans réparation — vert

```bash
sudo xfs_repair -n /dev/sdX1
```

Analyse sans écriture ; si un journal doit être rejoué, préparer une copie et consulter le guide.

### 2. Réparer la copie démontée — rouge

```bash
rescue-rw /dev/sdY &&
sudo xfs_repair /dev/sdY1
```

Écrit les métadonnées de la copie. Garder une copie avant réparation et le journal de sortie.

### 3. Borner la mémoire du contrôle — vert

```bash
sudo xfs_repair -n -m 128 /dev/sdX1
```

128 Mio est un budget indicatif pour une petite image ; ce réglage n’est pas une mesure de performance et peut ralentir un gros volume.

## Pièges

- Toujours démonter XFS ; une image doit être traitée avec -f. Prévoir de la mémoire et du temps sur un grand volume.
- -L détruit le journal et peut perdre des fichiers ; ne pas l’ajouter automatiquement après un refus.

## Voir aussi

`rescue-ro`, `rescue-rw`, `ddrescue`, guide 09.
