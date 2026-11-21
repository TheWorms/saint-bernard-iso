# lspci — identifier les cartes PCI et leur pilote

**Couleur : vert.** Inventaire PCI sans modification des registres.

**Lancer :** menu SOS, rubrique Matériel et système ; fenêtre `assistant-lspci` ; terminal : `lspci`.

Identifier les disques avec `lsblk -o NAME,SIZE,MODEL,SERIAL` avant de remplacer `sdX`, `sdY` ou `nvme0`. Les lectures intensives se font sur une copie ou un support sain. Ne jamais ouvrir l’original à récupérer avec `rescue-rw`.

## Usages

### 1. Afficher noms et identifiants numériques — vert

```bash
lspci -nn
```

Garder les identifiants fabricant:périphérique quand le nom humain est inconnu ou ambigu.

### 2. Associer cartes et pilotes du noyau — vert

```bash
lspci -nnk
```

Distinguer le pilote réellement utilisé des modules qui pourraient convenir.

### 3. Voir les ponts et la topologie — vert

```bash
lspci -t
```

Suivre les relations entre ponts et périphériques pour comprendre où se situe un contrôleur.

## Pièges

- Ne pas utiliser setpci pour un inventaire.
- Certaines capacités détaillées demandent plus de privilèges ; un accès refusé n’est pas une absence de carte.

## Voir aussi

`lshw`, `lsusb`, guide 03.
