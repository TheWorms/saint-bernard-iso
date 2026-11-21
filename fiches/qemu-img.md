# qemu-img — examiner et convertir une image virtuelle

**Couleur : rouge.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Images et machines virtuelles ; fenêtre `assistant-qemu-img` ; terminal : `qemu-img`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est la source protégée ; `sdY` une destination distincte. Pour l’analyse, préférer une copie ; ne jamais ouvrir l’original à récupérer avec `rescue-rw`. Les chemins en majuscules sont à remplacer après vérification.

## Usages

### 1. Lire la chaîne de fichiers parents — vert

```bash
qemu-img info -f qcow2 --backing-chain /mnt/COPIE/disque.qcow2
```

Vérifier format et fichiers parents. Les parents doivent tous être disponibles ; l’extension seule ne prouve pas le format.

### 2. Contrôler les métadonnées sans réparer — vert

```bash
qemu-img check -f qcow2 /mnt/COPIE/disque.qcow2
```

Ne pas ajouter -r. Un contrôle de conteneur ne teste pas l’intégrité du système de fichiers invité.

### 3. Convertir vers une nouvelle image brute — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
test ! -e /mnt/DESTINATION/TRAVAIL/disque-brut.img &&
qemu-img convert -f qcow2 -O raw /mnt/COPIE/disque.qcow2 /mnt/DESTINATION/TRAVAIL/disque-brut.img
```

Écrit un fichier neuf sur la destination ; la source reste inchangée. Prévoir la taille réelle de l’image brute, pas seulement celle du qcow2.

## Pièges

- Ne pas employer check -r, resize, amend ou commit sur l’image maître.
- Arrêter la VM propriétaire de l’image et conserver toute sa chaîne.

## Voir aussi

`qemu-nbd`, `guestmount`, guide 05.
