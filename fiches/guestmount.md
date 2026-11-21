# guestmount — monter une image avec libguestfs en RO

**Couleur : rouge.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Images et machines virtuelles ; fenêtre `assistant-guestmount` ; terminal : `sudo guestmount`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est la source protégée ; `sdY` une destination distincte. Pour l’analyse, préférer une copie ; ne jamais ouvrir l’original à récupérer avec `rescue-rw`. Les chemins en majuscules sont à remplacer après vérification.

## Usages

### 1. Monter une partition identifiée — vert

```bash
sudo guestmount --ro --format=qcow2 -a /mnt/COPIE/disque.qcow2 -m /dev/sda1 /mnt/LECTURE
```

Créer auparavant un point vide. /dev/sda1 désigne la partition dans l’appliance, pas le disque physique du live ; l’identifier avec virt-filesystems.

### 2. Utiliser l’inspection d’un système installé — vert

```bash
sudo guestmount --ro --format=qcow2 -a /mnt/COPIE/disque.qcow2 -i /mnt/LECTURE
```

-i exige un système d’exploitation reconnaissable. Une simple partition de données n’est pas suffisante.

### 3. Démonter le point FUSE suivi — vert

```bash
sudo guestunmount /mnt/LECTURE
```

Fermer les fenêtres et terminaux utilisant le point. Utiliser guestunmount avec les mêmes droits que le montage.

## Pièges

- Toujours --ro ; la VM d’origine doit être arrêtée pour une vue cohérente.
- Le démarrage de l’appliance peut dépasser le délai de banc sur un hôte lent ; ne pas appeler cela un succès.

## Voir aussi

`virt-filesystems`, `qemu-nbd`, guide 05.
