# dmidecode — lire les informations SMBIOS

**Couleur : vert.** Lecture des tables fournies par le firmware, sans mise à jour du BIOS.

**Lancer :** menu SOS, rubrique Matériel et système ; fenêtre `assistant-dmidecode` ; terminal : `sudo dmidecode`.

Identifier les disques avec `lsblk -o NAME,SIZE,MODEL,SERIAL` avant de remplacer `sdX`, `sdY` ou `nvme0`. Les lectures intensives se font sur une copie ou un support sain. Ne jamais ouvrir l’original à récupérer avec `rescue-rw`.

## Usages

### 1. Lire le BIOS déclaré — vert

```bash
sudo dmidecode -t bios
```

Relever version et date du firmware. Ces informations sont déclaratives et peuvent être incomplètes ou erronées.

### 2. Identifier le système — vert

```bash
sudo dmidecode -t system
```

Contient souvent modèle et numéro de série : ne pas joindre ce rapport brut à un ticket public.

### 3. Lire les emplacements mémoire — vert

```bash
sudo dmidecode -t memory
```

Relever slots, capacités et types déclarés ; cela ne teste pas les barrettes ni leurs erreurs.

## Pièges

- SMBIOS peut manquer ou mentir ; recouper avec lshw et les observations physiques.
- Les tables d’une VM décrivent son matériel virtuel.

## Voir aussi

`lshw`, `memtester`, guide 03.
