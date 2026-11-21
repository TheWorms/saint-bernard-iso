# freshclam — mettre à jour les signatures officielles

**Couleur : aucun.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Antivirus ; fenêtre `assistant-freshclam` ; terminal : `sudo freshclam`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une cible distincte, sacrifiable pour les effacements. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. `/tmp` et les rapports du live sont en RAM, perdus à l’arrêt. Un serveur distant doit être autorisé et son identité vérifiée.

## Usages

### 1. Mettre à jour la base du live — aucun

```bash
sudo freshclam --stdout
```

Télécharge les signatures dans /var/lib/clamav en RAM ; pas de mise à jour garantie sans réseau autorisé.

### 2. Mettre à jour une base privée temporaire — aucun

```bash
sudo install -d -o clamav -g clamav -m 0700 /tmp/base-clamav &&
sudo freshclam --datadir=/tmp/base-clamav --stdout
```

Le compte clamav doit pouvoir traverser et écrire le dossier. Scanner ensuite avec clamscan -d /tmp/base-clamav.

### 3. Diagnostiquer une panne DNS de mise à jour — aucun

```bash
sudo freshclam --no-dns --stdout
```

Remplace la vérification DNS des versions par HTTP ; ne supprime pas la validation cryptographique des bases. Toujours un accès réseau.

## Pièges

- Le téléchargement peut être volumineux et la base du live est en RAM ; vérifier place et mémoire.
- Une base invalide doit être refusée. Ne pas désactiver la vérification des signatures ni mettre des identifiants de proxy dans un rapport.

## Voir aussi

`rescue-ro`, `rescue-rw`, `sha256sum`, guide 13.
