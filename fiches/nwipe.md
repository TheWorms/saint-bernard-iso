# nwipe — effacer un support explicitement choisi

**Couleur : rouge.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Effacement ; fenêtre `assistant-nwipe` ; terminal : `sudo nwipe`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une cible distincte, sacrifiable pour les effacements. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. `/tmp` et les rapports du live sont en RAM, perdus à l’arrêt. Un serveur distant doit être autorisé et son identité vérifiée.

## Usages

### 1. Choisir et confirmer dans le terminal — rouge

```bash
rescue-rw /dev/sdY &&
sudo nwipe --method=zero --verify=last --noblank /dev/sdY
```

Relire modèle, série et taille, sélectionner seulement sdY puis confirmer dans le menu. Rapport dans le dossier courant en RAM si celui-ci est /tmp.

### 2. Passer des zéros et les vérifier — rouge

```bash
rescue-rw /dev/sdY &&
sudo nwipe --autonuke --nogui --method=zero --verify=last --noblank --PDFreportpath=/tmp /dev/sdY
```

Démarrage immédiat après la confirmation complète de sdY (nom, taille, série). La cible explicite est obligatoire ; jamais copier une variable vide.

### 3. Vérifier un disque déjà rempli de zéros — jaune

```bash
rescue-rw /dev/sdY &&
sudo nwipe --autonuke --nogui --method=verify_zero --verify=off --noblank --PDFreportpath=/tmp /dev/sdY
```

La méthode verify_zero lit seulement ; --noblank empêche la passe finale d’écriture. Le logiciel peut exiger une ouverture RW, donc utiliser exclusivement la cible sacrifiable confirmée.

## Pièges

- Ne brancher que la cible ; jamais --autonuke sans périphérique explicite : cela sélectionnerait tous les disques.
- L’écrasement ne prouve pas l’effacement des cellules remappées d’un SSD. Le rapport /tmp est à conserver ailleurs avant arrêt.

## Voir aussi

`rescue-ro`, `rescue-rw`, `sha256sum`, guide 11.
