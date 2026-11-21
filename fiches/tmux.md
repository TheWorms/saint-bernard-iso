# tmux — conserver une console et s’y rattacher

**Couleur : aucun.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Bureau ; fenêtre `assistant-tmux` ; terminal : `tmux`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une cible distincte, sacrifiable pour les effacements. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. `/tmp` et les rapports du live sont en RAM, perdus à l’arrêt. Un serveur distant doit être autorisé et son identité vérifiée.

## Usages

### 1. Créer une session nommée — aucun

```bash
tmux new -s copie
```

Y lancer la commande de copie puis se détacher avec Ctrl+b, d ; la commande continue.

### 2. Lister les sessions existantes — aucun

```bash
tmux ls
```

Repérer le nom avant d’ouvrir ou d’arrêter une session. L’essai utilise une socket privée, sans toucher aux sessions existantes.

### 3. Se rattacher à la copie en cours — aucun

```bash
tmux attach -t copie
```

Retrouver l’écran et vérifier la commande ; ne pas la relancer en parallèle si elle tourne déjà.

## Pièges

- Une session ne survit pas à l’arrêt du live ; conserver séparément cartes, journaux et résultats.
- Ctrl+b puis d détache ; exit termine le shell. Ne pas lancer kill-server sur le serveur partagé de quelqu’un d’autre.

## Voir aussi

`rescue-ro`, `rescue-rw`, `sha256sum`, guide 13.
