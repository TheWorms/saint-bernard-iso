# rescue-install — installer sur un disque dédié

**Couleur : rouge.** Crée ou remplace le système de Saint-Bernard sur une destination dédiée.

**Lancer :** menu SOS, rubrique Démarrage et Windows ; ou dans un terminal : `rescue-install`.

Dans les exemples, remplacer `sdX` et les chemins en majuscules après identification avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. Les outils qui en ont besoin demandent automatiquement les droits sudo.

## Usages

### 1. Installer sur un disque vide — rouge

```bash
lsblk -o NAME,SIZE,MODEL,SERIAL
rescue-rw /dev/sdX
rescue-install /dev/sdX
```

Partitionne et formate `/dev/sdX` : choisir un disque vide d’au moins 6 Gio par modèle, taille et série, jamais un disque à récupérer. Retaper le nom, la taille et la série demandés ; crée `SB-SYSTEME` et `RESCUE-DATA`.

### 2. Mettre à jour un disque déjà installé — rouge

```bash
lsblk -o NAME,SIZE,MODEL,SERIAL
rescue-rw /dev/sdX
rescue-install --mise-a-jour /dev/sdX
```

Remplace le système de `/dev/sdX`, conserve `RESCUE-DATA`. Contrôler modèle et série du disque installé et les confirmations ; démarrer depuis un autre support, jamais depuis celui à mettre à jour.

### 3. Choisir l’ISO et le chargement en mémoire — rouge

```bash
lsblk -o NAME,SIZE,MODEL,SERIAL
rescue-rw /dev/sdX
rescue-install /dev/sdX --iso /mnt/DESTINATION/saint-bernard.iso --toram
```

Écrit toute l’installation sur le disque vide `/dev/sdX` identifié par modèle et série, après les trois confirmations. L’ISO est lue sur un autre support ; `--toram` choisit un système chargé en mémoire au démarrage et demande assez de RAM.

## Pièges

- Ne jamais effacer préalablement un disque qui contient des données pour contourner un refus.
- Les garde-fous refusent le support de démarrage et une installation neuve sur un disque non vide. Sauvegarder les données avant toute maintenance.

## Voir aussi

`rescue-rw`, `rescue-ro`, guide 10.
