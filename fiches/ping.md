# ping — tester une réponse ICMP bornée

**Couleur : aucun.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Réseau ; fenêtre `assistant-ping` ; terminal : `ping`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une cible distincte, sacrifiable pour les effacements. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. `/tmp` et les rapports du live sont en RAM, perdus à l’arrêt. Un serveur distant doit être autorisé et son identité vérifiée.

## Usages

### 1. Vérifier la boucle locale — aucun

```bash
ping -c 2 -W 2 127.0.0.1
```

Teste la pile locale, sans sortir de la machine.

### 2. Forcer IPv4 et éviter la résolution des réponses — aucun

```bash
ping -4 -n -c 2 -W 2 127.0.0.1
```

Remplacer l’adresse locale par la passerelle autorisée pour tester le lien ; -n garde les adresses numériques.

### 3. Vérifier IPv6 localement — aucun

```bash
ping -6 -n -c 2 -W 2 ::1
```

Nécessite IPv6 activé ; un refus doit être diagnostiqué, pas remplacé par un faux succès.

## Pièges

- Une réponse ne prouve pas que SSH/SMB fonctionne ; un silence peut venir d’un filtrage ICMP.
- Limiter nombre et attente, utiliser seulement des adresses autorisées ; pas de test en boucle infinie.

## Voir aussi

`rescue-ro`, `rescue-rw`, `sha256sum`, guide 13.
