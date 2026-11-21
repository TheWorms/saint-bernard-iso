# virt-filesystems — inventorier les volumes d’une image

**Couleur : vert.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Images et machines virtuelles ; fenêtre `assistant-virt-filesystems` ; terminal : `sudo virt-filesystems`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est la source protégée ; `sdY` une destination distincte. Pour l’analyse, préférer une copie ; ne jamais ouvrir l’original à récupérer avec `rescue-rw`. Les chemins en majuscules sont à remplacer après vérification.

## Usages

### 1. Lire la vue complète avec les tailles — vert

```bash
sudo virt-filesystems --format=qcow2 -a /mnt/COPIE/disque.qcow2 --all --long -h
```

Liste blocs, partitions et systèmes de fichiers sans montage en écriture ; les tailles lisibles ne remplacent pas les octets exacts.

### 2. Lister seulement les systèmes de fichiers — vert

```bash
sudo virt-filesystems --format=qcow2 -a /mnt/COPIE/disque.qcow2 --filesystems
```

Choisir ensuite le périphérique interne pour guestmount ; ne pas supposer que la première partition est celle recherchée.

### 3. Relier partitions et périphériques internes — vert

```bash
sudo virt-filesystems --format=qcow2 -a /mnt/COPIE/disque.qcow2 --partitions --block-devices --long
```

Les noms appartiennent à l’appliance. Recouper avec les systèmes de fichiers avant toute extraction.

## Pièges

- Un format non précisé peut être mal interprété ; sélectionner le format connu.
- Un inventaire ne répare ni ne valide les fichiers de l’invité.

## Voir aussi

`guestmount`, `qemu-img`, guide 05.
