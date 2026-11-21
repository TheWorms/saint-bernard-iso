# ms-sys — lire ou remplacer un code MBR Microsoft

**Couleur : rouge.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Démarrage et Windows ; fenêtre `assistant-ms-sys` ; terminal : `sudo ms-sys`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une cible distincte, sacrifiable pour les effacements. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. `/tmp` et les rapports du live sont en RAM, perdus à l’arrêt. Un serveur distant doit être autorisé et son identité vérifiée.

## Usages

### 1. Identifier le code présent sans écrire — vert

```bash
sudo ms-sys /dev/sdX
```

Sans option de code, identifie seulement le secteur de démarrage.

### 2. Écrire un MBR Windows 7 sur une copie — rouge

```bash
rescue-rw /dev/sdY &&
sudo ms-sys -7 /dev/sdY
```

Copie MBR sacrifiable, démontée. Vérifier partition active, capacité et sauvegarde de table avant écriture.

### 3. Écrire un MBR Windows 2000/XP sur une copie — rouge

```bash
rescue-rw /dev/sdY &&
sudo ms-sys -m /dev/sdY
```

Même précaution, pour le cas ancien correspondant ; aucun système UEFI n’est réparé par ce code.

## Pièges

- Disque MBR seulement, jamais GPT. Le code ne restaure ni table, ni fichiers, ni BCD.
- Sélectionner la partition active et le bon code après sauvegarde ; ne jamais employer l’option de forçage pour écrire un original.

## Voir aussi

`rescue-ro`, `rescue-rw`, `sha256sum`, guide 10.
