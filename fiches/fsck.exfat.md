# fsck.exfat — contrôler et réparer exFAT sur une copie

**Couleur : rouge.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Systèmes de fichiers ; fenêtre `assistant-fsck.exfat` ; terminal : `sudo fsck.exfat`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une copie de travail distincte, démontée et sacrifiable. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. Les fichiers de `/tmp` sont en mémoire et disparaissent à l’arrêt.

## Usages

### 1. Contrôler sans réparation — vert

```bash
sudo fsck.exfat -n /dev/sdX1
```

Diagnostic non interactif ; aucune écriture.

### 2. Réparer les cas sûrs sur une copie — rouge

```bash
rescue-rw /dev/sdY &&
sudo fsck.exfat -p /dev/sdY1
```

Copie démontée ; l’option -p limite les décisions automatiques, sans garantir la conservation de tous les fichiers.

### 3. Accepter les réparations sur une copie sacrifiable — rouge

```bash
rescue-rw /dev/sdY &&
sudo fsck.exfat -y /dev/sdY1
```

Dernier recours sur une copie dont une sauvegarde existe ; toutes les questions reçoivent oui. Relire le journal et comparer les fichiers.

## Pièges

- Démonter d’abord ; ne pas confondre exFAT et FAT32.
- -y accepte toutes les propositions, y compris celles qui perdent des données ; préférer l’extraction et une copie avant réparation.

## Voir aussi

`rescue-ro`, `rescue-rw`, `ddrescue`, guide 09.
