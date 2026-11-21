# pv — suivre un transfert de fichiers sains

**Couleur : aucun.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Clonage et images ; fenêtre `assistant-pv` ; terminal : `pv`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est la source protégée ; `sdY` une destination distincte. Pour l’analyse, préférer une copie ; ne jamais ouvrir l’original à récupérer avec `rescue-rw`. Les chemins en majuscules sont à remplacer après vérification.

## Usages

### 1. Copier avec suivi de progression — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
pv /mnt/COPIE/disque.img > /mnt/DESTINATION/TRAVAIL/disque-neuf.img
```

Le sous-dossier appartient à rescue : la redirection peut y créer le fichier. Choisir un nom neuf et vérifier ensuite les empreintes.

### 2. Limiter le débit du transfert — orange

```bash
rescue-rw /dev/sdY &&
rescue-mount --ecriture /dev/sdY1 /mnt/DESTINATION &&
sudo install -d -o rescue -g rescue -m 0700 /mnt/DESTINATION/TRAVAIL &&
pv -L 10m /mnt/COPIE/disque.img > /mnt/DESTINATION/TRAVAIL/disque-limite.img
```

Limite à environ 10 Mio/s pour laisser de la marge aux autres opérations ; ce n’est pas une limite de durée.

### 3. Suivre le calcul d’empreinte — vert

```bash
set -o pipefail
pv /mnt/COPIE/disque.img | sha256sum
```

Le tube ne change pas l’image. pipefail empêche de confondre une lecture incomplète avec l’empreinte normale.

## Pièges

- Ne jamais utiliser pv pour remplacer la reprise sur erreurs de ddrescue.
- sudo devant pv ne donne pas les droits à une redirection du shell ; préparer une destination accessible.

## Voir aussi

`sha256sum`, `ddrescue`, guide 04.
