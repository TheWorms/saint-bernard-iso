# losetup — présenter une image en lecture seule

**Couleur : vert.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Clonage et images ; fenêtre `assistant-losetup` ; terminal : `sudo losetup`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est la source protégée ; `sdY` une destination distincte. Pour l’analyse, préférer une copie ; ne jamais ouvrir l’original à récupérer avec `rescue-rw`. Les chemins en majuscules sont à remplacer après vérification.

## Usages

### 1. Attacher l’image et ses partitions en RO — vert

```bash
sudo losetup --find --show --read-only --partscan /mnt/COPIE/disque.img
```

Noter le /dev/loopN renvoyé. L’image brute est lue sans ouvrir l’écriture ; ne pas appliquer cela à un format qcow2.

### 2. Retrouver le fichier associé — vert

```bash
sudo losetup --list --output NAME,BACK-FILE,RO /dev/loopN
```

Remplacer loopN par l’attachement créé. Vérifier chemin et RO avant de lire une partition.

### 3. Détacher seulement sa propre boucle — vert

```bash
sudo losetup --detach /dev/loopN
```

Démonter d’abord tout point utilisant cette boucle. Ne pas employer --detach-all sur une session de récupération.

## Pièges

- Une partition loopNp1 n’est pas l’attachement parent loopN.
- Un détachement peut être différé tant qu’un processus tient le périphérique.

## Voir aussi

`qemu-nbd`, `rescue-umount`, guide 04.
