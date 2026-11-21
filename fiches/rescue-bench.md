# rescue-bench — mesurer la lecture d’un disque

**Couleur : jaune.** Lecture intensive, sans écriture sur le disque mesuré.

**Lancer :** menu SOS, rubrique Tests et mesures ; ou dans un terminal : `rescue-bench`.

Dans les exemples, remplacer `sdX` et les chemins en majuscules après identification avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. Les outils qui en ont besoin demandent automatiquement les droits sudo.

## Usages

### 1. Mesurer débit et latence — jaune

```bash
rescue-bench /dev/sdX
```

Choisir un disque stable par modèle et série. Mesure début, milieu et fin si sa taille le permet, puis dix lectures de latence ; un SMART critique bloque l’opération.

### 2. Garder les mesures sur la destination — orange

```bash
rescue-bench /dev/sdX | tee /mnt/DESTINATION/mesures.txt
```

Lit intensivement `/dev/sdX` et écrit seulement `mesures.txt` sur la destination déjà montée en écriture après `rescue-rw`. Vérifier avec `lsblk -o NAME,SIZE,MODEL,SERIAL` que cette destination est un autre disque sain, puis contrôler `findmnt /mnt/DESTINATION`.

### 3. Lire les options avant de commencer — vert

```bash
rescue-bench --help
```

Affiche l’aide de la commande sans agir sur un disque.

## Pièges

- Bruits, erreurs ou déconnexions : cloner d’abord, ne pas comparer les débits.
- Les chiffres de QEMU mesurent le stockage virtuel ; comparer les performances réelles sur la machine témoin.

## Voir aussi

`rescue-smart`, `rescue-clone`, guide 01.
