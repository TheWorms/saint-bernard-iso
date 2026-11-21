# efibootmgr — lire et modifier les entrées UEFI

**Couleur : rouge.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Démarrage et Windows ; fenêtre `assistant-efibootmgr` ; terminal : `sudo efibootmgr`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une cible distincte, sacrifiable pour les effacements. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. `/tmp` et les rapports du live sont en RAM, perdus à l’arrêt. Un serveur distant doit être autorisé et son identité vérifiée.

## Usages

### 1. Lire les entrées et leurs chemins — vert

```bash
sudo efibootmgr -v
```

Session démarrée en UEFI avec efivarfs disponible ; conserver BootCurrent et BootOrder.

### 2. Choisir seulement le prochain démarrage — rouge

```bash
sudo efibootmgr -n 0003
```

0003 est un exemple : relire -v puis choisir une entrée existante confirmée. Modifie BootNext, pas BootOrder.

### 3. Modifier l’ordre persistant — rouge

```bash
sudo efibootmgr -o 0003,0001
```

Exemples de numéros à remplacer ; conserver les autres entrées voulues et noter l’ordre d’origine pour revenir en arrière.

## Pièges

- La NVRAM n’est pas protégée par rescue-ro et une écriture ne demande pas rescue-rw ; ne pas l’expérimenter sur le firmware de production.
- BootNext est temporaire, BootOrder est durable. Photographier l’état initial et ne jamais choisir un numéro inventé.

## Voir aussi

`rescue-ro`, `rescue-rw`, `sha256sum`, guide 10.
