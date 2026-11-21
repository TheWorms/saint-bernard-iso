# os-prober — chercher les systèmes sur des copies

**Couleur : jaune.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Démarrage et Windows ; fenêtre `assistant-os-prober` ; terminal : `sudo os-prober`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une cible distincte, sacrifiable pour les effacements. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. `/tmp` et les rapports du live sont en RAM, perdus à l’arrêt. Un serveur distant doit être autorisé et son identité vérifiée.

## Usages

### 1. Chercher les systèmes installés — jaune

```bash
sudo os-prober
```

Les disques restent en lecture seule ; le programme peut monter temporairement des partitions pour identifier les OS.

### 2. Conserver le résultat dans le live — jaune

```bash
sudo os-prober > /tmp/os-prober.txt
```

Rapport dans la RAM, à exporter avant l’arrêt. Chaque ligne indique partition, nom, type et chargeur.

### 3. Lire les paramètres d’un Linux détecté — jaune

```bash
sudo linux-boot-prober /dev/sdX1
```

Compagnon d’os-prober, sur une partition Linux de copie identifiée. Peut monter la partition ; ne pas autoriser l’écriture de l’original.

## Pièges

- os-prober monte des partitions : ce n’est pas une lecture brute passive. Garder tous les originaux protégés et travailler sur des copies.
- Un résultat vide ne démontre pas l’absence de système ; le live et les volumes chiffrés peuvent être ignorés.

## Voir aussi

`rescue-ro`, `rescue-rw`, `sha256sum`, guide 10.
