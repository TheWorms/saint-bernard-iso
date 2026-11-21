# chntpw — examiner un SAM et préparer une copie autorisée

**Couleur : rouge.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Démarrage et Windows ; fenêtre `assistant-chntpw` ; terminal : `sudo chntpw`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une cible distincte, sacrifiable pour les effacements. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. `/tmp` et les rapports du live sont en RAM, perdus à l’arrêt. Un serveur distant doit être autorisé et son identité vérifiée.

## Usages

### 1. Lister les comptes sans modifier la ruche — vert

```bash
sudo chntpw -l /tmp/SAM
```

Copie du SAM extraite en lecture seule depuis le volume Windows ; /tmp disparaît à l’arrêt.

### 2. Explorer puis quitter sans enregistrer — vert

```bash
sudo chntpw -e /tmp/SAM
```

Dans l’éditeur : ls pour lister, q pour sortir ; refuser tout enregistrement si une modification involontaire a été faite.

### 3. Vider le mot de passe sur une copie du SAM — rouge

```bash
sudo cp /tmp/SAM /tmp/SAM-travail &&
sudo chntpw -u NOM_COMPTE /tmp/SAM-travail
```

Écrit seulement une copie en RAM : choisir 1 pour vider, q puis y pour enregistrer. Ne définit pas de nouveau mot de passe. La remise sur un clone Windows démonté exige une procédure séparée du guide, jamais sur l’original.

## Pièges

- Accord du propriétaire indispensable ; comptes locaux seulement, pas comptes Microsoft ni BitLocker.
- Le SAM fictif du banc contient un compte déjà vide ; il ne prouve pas l’effacement d’un mot de passe. Garder les ruches d’avant intervention.

## Voir aussi

`rescue-ro`, `rescue-rw`, `sha256sum`, guide 10.
