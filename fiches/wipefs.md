# wipefs — lire ou retirer des signatures

**Couleur : rouge.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Effacement ; fenêtre `assistant-wipefs` ; terminal : `sudo wipefs`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une cible distincte, sacrifiable pour les effacements. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. `/tmp` et les rapports du live sont en RAM, perdus à l’arrêt. Un serveur distant doit être autorisé et son identité vérifiée.

## Usages

### 1. Lister les signatures et leurs positions — vert

```bash
sudo wipefs --output DEVICE,OFFSET,TYPE /dev/sdX
```

Aucune option d’effacement ; inventaire en lecture seule.

### 2. Simuler leur suppression — vert

```bash
sudo wipefs --all --no-act /dev/sdX
```

--no-act interdit les écritures ; relire les positions et le type.

### 3. Supprimer avec sauvegarde des signatures — rouge

```bash
rescue-rw /dev/sdY &&
sudo install -d -m 0700 /tmp/signatures-avant &&
sudo wipefs --all --backup=/tmp/signatures-avant /dev/sdY1
```

Copie démontée uniquement. /tmp est volatile : exporter la sauvegarde avant l’arrêt ; elle ne remplace pas une image complète.

## Pièges

- Retirer une signature n’efface pas les données ; ce n’est pas une suppression sécurisée.
- Sur un disque partitionné, --all vise sa table, pas tous les contenus des partitions ; sauvegarder les signatures et la table avant action.

## Voir aussi

`rescue-ro`, `rescue-rw`, `sha256sum`, guide 11.
