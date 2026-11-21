# clamscan — analyser une copie sans supprimer

**Couleur : jaune.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Antivirus ; fenêtre `assistant-clamscan` ; terminal : `clamscan`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une cible distincte, sacrifiable pour les effacements. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. `/tmp` et les rapports du live sont en RAM, perdus à l’arrêt. Un serveur distant doit être autorisé et son identité vérifiée.

## Usages

### 1. Analyser récursivement sans action — jaune

```bash
clamscan -r -i /mnt/COPIE/recuperation
```

Copie ou disque sain : lecture complète des fichiers ; aucune suppression. Nécessite une base installée.

### 2. Utiliser une base hors ligne et garder le rapport — jaune

```bash
clamscan -d /mnt/ARCHIVES/clamav-db -r -i -l /tmp/clamscan.txt /mnt/COPIE/recuperation
```

Base de confiance conservée séparément ; exporter le rapport RAM. L’essai utilise uniquement une signature textuelle fictive, pas un virus.

### 3. Déplacer une détection sur la copie de travail — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
mkdir /mnt/DESTINATION/TRAVAIL/quarantaine &&
clamscan -r -i --move=/mnt/DESTINATION/TRAVAIL/quarantaine /mnt/DESTINATION/TRAVAIL/recuperation
```

Modifie exclusivement les fichiers récupérés sur la destination ouverte RW. Garder une autre copie et relire les détections avant toute suppression.

## Pièges

- Code 0 : rien trouvé ; 1 : détection ; 2 : erreur. Une erreur ou une base absente n’est pas un résultat sain.
- Une détection n’est pas une preuve de compromission et une absence de détection ne garantit rien ; ne pas utiliser --remove sur les originaux.

## Voir aussi

`rescue-ro`, `rescue-rw`, `sha256sum`, guide 13.
