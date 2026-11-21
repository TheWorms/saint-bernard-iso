# lsusb — inventorier les périphériques USB

**Couleur : vert.** Consultation des identités et de la topologie USB.

**Lancer :** menu SOS, rubrique Matériel et système ; fenêtre `assistant-lsusb` ; terminal : `lsusb`.

Identifier les disques avec `lsblk -o NAME,SIZE,MODEL,SERIAL` avant de remplacer `sdX`, `sdY` ou `nvme0`. Les lectures intensives se font sur une copie ou un support sain. Ne jamais ouvrir l’original à récupérer avec `rescue-rw`.

## Usages

### 1. Lire les identifiants USB — vert

```bash
lsusb
```

Relever bus, numéro de périphérique et identifiants fabricant:produit ; les numéros changent après reconnexion.

### 2. Voir le pilote et la vitesse de chaque port — vert

```bash
lsusb -t
```

Repérer les hubs et lire la vitesse négociée, pas seulement la vitesse théorique de la prise.

### 3. Ajouter les identités à l’arbre — vert

```bash
lsusb -t -v
```

Combine la topologie avec les noms et identifiants disponibles, sans débrancher un support de récupération.

## Pièges

- Une lenteur USB peut venir du câble, du hub ou de l’alimentation ; ne pas relancer des tests sur un disque instable.
- Ne pas confondre identifiant USB du pont et numéro de série du disque derrière lui.

## Voir aussi

`lsblk`, `lspci`, guide 03.
