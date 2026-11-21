# lsblk — identifier les disques et leurs partitions

**Couleur : vert.** Inventaire sans ouvrir l’écriture sur les disques.

**Lancer :** menu SOS, rubrique Diagnostic des disques ; fenêtre `assistant-lsblk` ; terminal : `lsblk`.

Identifier les disques avec `lsblk -o NAME,SIZE,MODEL,SERIAL` avant de remplacer `sdX`, `sdY` ou `nvme0`. Les lectures intensives se font sur une copie ou un support sain. Ne jamais ouvrir l’original à récupérer avec `rescue-rw`.

## Usages

### 1. Identifier par modèle et série — vert

```bash
lsblk -d -o NAME,PATH,SIZE,ROTA,TRAN,MODEL,SERIAL,RO
```

Faire correspondre modèle, série et taille avec le support physique ; sdX peut changer après un débranchement.

### 2. Voir partitions et montages — vert

```bash
lsblk -o NAME,SIZE,TYPE,FSTYPE,LABEL,RO,MOUNTPOINTS
```

Lire l’arbre complet avant de choisir une partition. Une colonne vide peut simplement indiquer une information non détectée.

### 3. Relier une partition au disque parent — vert

```bash
lsblk -o NAME,PKNAME,TYPE,SIZE,RO /dev/sdX
```

PKNAME identifie le parent. Ne pas confondre le disque entier avec une de ses partitions.

### 4. Obtenir un inventaire JSON explicite — vert

```bash
lsblk --json -o NAME,TYPE,SIZE,RO /dev/sdX
```

Fixer les colonnes pour les scripts ; le format et les colonnes par défaut ne sont pas une interface stable.

## Pièges

- RO décrit le drapeau du noyau, pas une garantie de santé ou de protection contre toutes les commandes du contrôleur.
- Consulter findmnt pour confirmer un montage précis.

## Voir aussi

`blockdev`, `rescue-disks`, guide 01.
