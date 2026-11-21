# ocs-sr — sauvegarder et restaurer avec Clonezilla

**Couleur : orange.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Clonage et images ; fenêtre `assistant-ocs-sr` ; terminal : `sudo ocs-sr`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est la source protégée ; `sdY` une destination distincte. Pour l’analyse, préférer une copie ; ne jamais ouvrir l’original à récupérer avec `rescue-rw`. Les chemins en majuscules sont à remplacer après vérification.

## Usages

### 1. Sauvegarder un disque sain — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/partimag &&
sudo ocs-sr -q2 -c -j2 -z1p -i 4096 -sfsck -senc -p choose savedisk NOM-IMAGE sdX
```

Le dépôt /mnt/partimag est sur sdY, distinct de sdX, sain et assez grand. Clonezilla demande confirmation ; utiliser une copie stable, pas un original fragile.

### 2. Sauvegarder des partitions choisies — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/partimag &&
sudo ocs-sr -q2 -c -z1p -sfsck -senc -p choose saveparts NOM-IMAGE "sdX1 sdX2"
```

Les noms de partitions sont sans /dev/. Choisir des partitions démontées ; cette archive ne remplace pas toujours une sauvegarde complète de l’amorçage.

### 3. Restaurer vers un disque dédié — rouge

```bash
rescue-rw /dev/sdY &&
sudo ocs-sr -c -p choose restoredisk NOM-IMAGE sdY
```

Le dépôt /mnt/partimag contenant NOM-IMAGE est déjà monté depuis un autre disque. Écrase sdY et sa table : identifier la cible et confirmer uniquement le support sacrifiable.

## Pièges

- savedisk/saveparts lisent la source ; restoredisk écrit la cible entière.
- Ne pas désactiver les contrôles d’image pour faire tenir une recette dans un délai.

## Voir aussi

`rescue-clone`, `fsarchiver`, guide 04.
