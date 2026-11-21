# blockdev — consulter taille, secteurs et protection

**Couleur : vert.** Uniquement des opérations de consultation dans cette fiche.

**Lancer :** menu SOS, rubrique Diagnostic des disques ; fenêtre `assistant-blockdev` ; terminal : `sudo blockdev`.

Identifier les disques avec `lsblk -o NAME,SIZE,MODEL,SERIAL` avant de remplacer `sdX`, `sdY` ou `nvme0`. Les lectures intensives se font sur une copie ou un support sain. Ne jamais ouvrir l’original à récupérer avec `rescue-rw`.

## Usages

### 1. Lire la taille exacte en octets — vert

```bash
sudo blockdev --getsize64 /dev/sdX
```

Comparer les octets avec la taille de l’image attendue ; ne pas confondre cette valeur avec un nombre de secteurs.

### 2. Lire les tailles de secteur — vert

```bash
sudo blockdev --getss --getpbsz /dev/sdX
```

La première ligne donne le secteur logique, la seconde le secteur physique annoncé. Ne pas supposer que tous valent 512 octets.

### 3. Vérifier la protection RO — vert

```bash
sudo blockdev --getro /dev/sdX
```

1 signifie lecture seule ; 0 signifie que le noyau autorise l’écriture. Ne pas employer --setrw pour contourner rescue-rw.

### 4. Comparer le résumé du périphérique — vert

```bash
sudo blockdev --report /dev/sdX
```

Le rapport présente RO, tailles de bloc et taille totale ; il n’examine pas l’état des données.

## Pièges

- Un drapeau RO ne bloque pas tous les autotests ou commandes internes du contrôleur.
- Pour changer l’accès en écriture, rester dans le cadre rescue-rw/rescue-ro.

## Voir aussi

`lsblk`, `rescue-ro`, `rescue-rw`, guide 01.
