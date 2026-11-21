# e2fsck — contrôler et réparer ext2/ext3/ext4 sur une copie

**Couleur : rouge.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Systèmes de fichiers ; fenêtre `assistant-e2fsck` ; terminal : `sudo e2fsck`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une copie de travail distincte, démontée et sacrifiable. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. Les fichiers de `/tmp` sont en mémoire et disparaissent à l’arrêt.

## Usages

### 1. Contrôler sans modifier — vert

```bash
sudo e2fsck -f -n /dev/sdX1
```

Sur partition démontée. Les erreurs sont signalées sans réparation ; commencer par sauver les données lisibles.

### 2. Réparer seulement les cas automatiques — rouge

```bash
rescue-rw /dev/sdY &&
sudo e2fsck -f -p /dev/sdY1
```

Copie démontée. -p refuse les décisions risquées ; si le code est 4, analyser au lieu de passer aveuglément à -y.

### 3. Répondre aux réparations proposées — rouge

```bash
rescue-rw /dev/sdY &&
sudo e2fsck -f /dev/sdY1
```

Copie démontée ; lire chaque question et conserver une copie avant réparation. L’essai fournit les réponses sous pseudo-terminal pour une incohérence connue.

## Pièges

- Toujours démonter la partition avant contrôle ; -n ne rend pas fiable le contrôle d’un volume monté.
- Les codes sont un masque : 1 signifie corrigé, 2 redémarrage requis, 4 erreurs restantes ; garder le journal et relire le résultat.

## Voir aussi

`rescue-ro`, `rescue-rw`, `ddrescue`, guide 09.
