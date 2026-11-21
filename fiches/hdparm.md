# hdparm — identifier un disque ATA et mesurer sa lecture

**Couleur : vert.** L’identité et l’état RO se lisent sans écriture ; le débit sollicite intensivement le disque.

**Lancer :** menu SOS, rubriques Diagnostic des disques, Tests et mesures, Effacement ; fenêtre `assistant-hdparm` ; terminal : `sudo hdparm`.

Identifier les disques avec `lsblk -o NAME,SIZE,MODEL,SERIAL` avant de remplacer `sdX`, `sdY` ou `nvme0`. Les lectures intensives se font sur une copie ou un support sain. Ne jamais ouvrir l’original à récupérer avec `rescue-rw`.

## Usages

### 1. Lire l’identité ATA — vert

```bash
sudo hdparm -I /dev/sdX
```

Lire modèle, série et fonctions déclarées. Un pont USB peut refuser cette interrogation ; ne pas contourner le refus par une commande d’effacement.

### 2. Consulter le drapeau de lecture seule — vert

```bash
sudo hdparm -r /dev/sdX
```

Sans valeur après -r, cette commande consulte seulement le drapeau. Pour ouvrir ou refermer l’écriture, utiliser rescue-rw ou rescue-ro, pas -r0.

### 3. Mesurer la lecture sans le cache Linux — jaune

```bash
sudo hdparm -t --direct /dev/sdX
```

Uniquement sur une copie ou un disque stable identifié. Répéter pour comparer ; arrêter si erreurs, bruits ou déconnexions. Les chiffres QEMU sont ceux du stockage virtuel.

### 4. Mesurer le cache et la mémoire — jaune

```bash
sudo hdparm -T /dev/sdX
```

Ce test mesure principalement le cache et la mémoire, pas le débit physique du disque ; ne pas l’utiliser comme verdict de santé.

## Pièges

- Les options security-erase, de mot de passe ATA et de géométrie ne font pas partie de cette fiche.
- La lecture seule du noyau n’interdit pas les commandes d’effacement internes ATA.

## Voir aussi

`blockdev`, `rescue-smart`, `rescue-clone`, guides 01 et 12.
