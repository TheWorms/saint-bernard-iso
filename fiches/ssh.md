# ssh — ouvrir une session avec identité vérifiée

**Couleur : aucun.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Réseau ; fenêtre `assistant-ssh` ; terminal : `ssh`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une cible distincte, sacrifiable pour les effacements. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. `/tmp` et les rapports du live sont en RAM, perdus à l’arrêt. Un serveur distant doit être autorisé et son identité vérifiée.

## Usages

### 1. Ouvrir une session autorisée — aucun

```bash
ssh UTILISATEUR@SERVEUR
```

Vérifier l’identité avant d’accepter la première clé ; utiliser exit pour fermer. L’essai exécute id dans une session locale à clé connue.

### 2. Créer un dossier distant privé — orange

```bash
ssh UTILISATEUR@SERVEUR 'mkdir -p -m 700 /CHEMIN/intervention-AAAA-MM-JJ'
```

Écrit seulement sur le serveur autorisé. Choisir un dossier neuf et propre à l’intervention.

### 3. Vérifier une empreinte après transfert — aucun

```bash
ssh UTILISATEUR@SERVEUR 'cd /CHEMIN/intervention-AAAA-MM-JJ && sha256sum -c source.img.sha256'
```

Le manifeste doit provenir du transfert voulu ; comparer le résultat, pas seulement l’ouverture de session.

## Pièges

- Comparer l’empreinte du serveur par un canal connu ; ne pas désactiver StrictHostKeyChecking pour effacer un avertissement.
- Une commande distante agit avec les droits du compte distant. Ne pas mettre mot de passe ou clé privée dans un rapport.

## Voir aussi

`rescue-ro`, `rescue-rw`, `sha256sum`, guide 13.
