# nvme — identifier un SSD NVMe et lire ses journaux

**Couleur : vert.** Usages de diagnostic uniquement ; format et sanitize détruisent des données.

**Lancer :** menu SOS, rubriques Diagnostic des disques, Effacement ; fenêtre `assistant-nvme` ; terminal : `sudo nvme`.

Identifier les disques avec `lsblk -o NAME,SIZE,MODEL,SERIAL` avant de remplacer `sdX`, `sdY` ou `nvme0`. Les lectures intensives se font sur une copie ou un support sain. Ne jamais ouvrir l’original à récupérer avec `rescue-rw`.

## Usages

### 1. Lister les espaces de noms — vert

```bash
sudo nvme list
```

Relever le contrôleur, les espaces de noms, modèle et série. Remplacer ensuite nvme0 par le contrôleur identifié ; une liste vide ne prouve pas l’absence de disque SATA ou USB.

### 2. Lire l’identité du contrôleur — vert

```bash
sudo nvme id-ctrl -H /dev/nvme0
```

Décode les capacités du contrôleur, sans lancer de formatage ni modifier sa configuration.

### 3. Lire santé et température — vert

```bash
sudo nvme smart-log /dev/nvme0
```

Lire avertissements critiques, usure, température et erreurs. Un journal sans alerte ne garantit pas la récupération des données.

### 4. Lire les dernières erreurs — vert

```bash
sudo nvme error-log /dev/nvme0
```

Comparer au contexte et aux compteurs de santé ; une commande non prise en charge peut aussi remplir ce journal.

## Pièges

- Ne pas employer format ou sanitize dans une opération de récupération.
- Un contrôleur nvme0 peut desservir plusieurs espaces de noms ; vérifier les identités avant tout autre outil.

## Voir aussi

`smartctl`, `lsblk`, guides 01 et 12.
