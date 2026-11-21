# ip — lire les interfaces et les routes

**Couleur : aucun.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Réseau ; fenêtre `assistant-ip` ; terminal : `ip`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une cible distincte, sacrifiable pour les effacements. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. `/tmp` et les rapports du live sont en RAM, perdus à l’arrêt. Un serveur distant doit être autorisé et son identité vérifiée.

## Usages

### 1. Lister les liens — aucun

```bash
ip -br link
```

Repérer les interfaces ; aucune activation n’est effectuée.

### 2. Lister les adresses — aucun

```bash
ip -br addr
```

Lire adresses et préfixes, sans en attribuer. Ne pas confondre adresse locale et passerelle.

### 3. Lire la route choisie sans envoyer de paquet — aucun

```bash
ip route get 127.0.0.1
```

Exemple local sans réseau extérieur ; remplacer par une adresse autorisée pour diagnostiquer le routage.

## Pièges

- Les lectures ne configurent pas le réseau. Ne pas ajouter link set, addr add ou route add sans décision explicite.
- Un lien UP ne prouve ni DNS ni accès au serveur ; rester sur le réseau autorisé.

## Voir aussi

`rescue-ro`, `rescue-rw`, `sha256sum`, guide 13.
