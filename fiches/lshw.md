# lshw — inventorier le matériel

**Couleur : vert.** Consultation de l’inventaire ; les rapports peuvent contenir des identifiants.

**Lancer :** menu SOS, rubrique Matériel et système ; fenêtre `assistant-lshw` ; terminal : `sudo lshw`.

Identifier les disques avec `lsblk -o NAME,SIZE,MODEL,SERIAL` avant de remplacer `sdX`, `sdY` ou `nvme0`. Les lectures intensives se font sur une copie ou un support sain. Ne jamais ouvrir l’original à récupérer avec `rescue-rw`.

## Usages

### 1. Lire le résumé matériel — vert

```bash
sudo lshw -short
```

Relever processeur, mémoire, contrôleurs et disques, sans lancer de benchmark.

### 2. Isoler les éléments mémoire — vert

```bash
sudo lshw -short -class memory
```

Distinguer la mémoire déclarée du total réellement disponible pour les applications.

### 3. Isoler disques et contrôleurs de stockage — vert

```bash
sudo lshw -class disk -class storage
```

Lire bus et pilote ; confirmer l’identité d’un disque avec lsblk avant toute action ultérieure.

### 4. Créer un rapport HTML anonymisé dans le live — vert

```bash
sudo lshw -sanitize -html > /tmp/materiel.html
```

Le rapport est écrit en RAM dans /tmp. Relire son contenu avant partage : l’anonymisation n’exonère pas de vérifier les informations restantes.

## Pièges

- Sans sudo, l’inventaire peut être incomplet ; ne pas prendre les éléments manquants pour du matériel absent.
- Un rapport HTML dans /tmp disparaît à l’arrêt ; conserver une copie sur une destination autorisée si nécessaire.

## Voir aussi

`dmidecode`, `lspci`, `lsusb`, guide 03.
