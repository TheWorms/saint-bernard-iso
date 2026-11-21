# qemu-nbd — exposer une image virtuelle en lecture seule

**Couleur : orange.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Images et machines virtuelles ; fenêtre `assistant-qemu-nbd` ; terminal : `sudo qemu-nbd`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est la source protégée ; `sdY` une destination distincte. Pour l’analyse, préférer une copie ; ne jamais ouvrir l’original à récupérer avec `rescue-rw`. Les chemins en majuscules sont à remplacer après vérification.

## Usages

### 1. Attacher une image à un NBD libre — vert

```bash
sudo modprobe nbd max_part=16 &&
sudo qemu-nbd --read-only --format=qcow2 --connect=/dev/nbd0 /mnt/COPIE/disque.qcow2
```

Choisir un NBD réellement libre, pas une connexion existante. Le format est explicite et --read-only protège l’image.

### 2. Servir une image par socket Unix privée — vert

```bash
sudo qemu-nbd --read-only --persistent --format=qcow2 --socket=/tmp/nbd-lecture.sock /mnt/COPIE/disque.qcow2
```

Service local au premier plan, sans port réseau. Le laisser seulement le temps des clients puis l’arrêter dans son terminal.

### 3. Détacher uniquement sa connexion — vert

```bash
sudo qemu-nbd --disconnect /dev/nbd0
```

Démonter d’abord ses partitions ; ne jamais déconnecter un NBD appartenant à une autre opération.

## Pièges

- Ne pas exposer une image inconnue en écriture.
- Le module nbd peut être absent tant que modprobe n’a pas été lancé.

## Voir aussi

`losetup`, `virt-filesystems`, guide 05.
