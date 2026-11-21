# badblocks — lire la surface d’une copie

**Couleur : jaune.** Lecture intensive ; les options -n et -w écrivent et ne sont pas utilisées ici.

**Lancer :** menu SOS, rubrique Tests et mesures ; fenêtre `assistant-badblocks` ; terminal : `sudo badblocks`.

Identifier les disques avec `lsblk -o NAME,SIZE,MODEL,SERIAL` avant de remplacer `sdX`, `sdY` ou `nvme0`. Les lectures intensives se font sur une copie ou un support sain. Ne jamais ouvrir l’original à récupérer avec `rescue-rw`.

## Usages

### 1. Lire toute une copie stable — jaune

```bash
sudo badblocks -sv -b 4096 /dev/sdX
```

sdX désigne ici une copie ou un disque sain, démonté. Ne pas multiplier les lectures d’un original fragile : cloner d’abord.

### 2. Limiter la lecture aux premiers 32 Mio — jaune

```bash
sudo badblocks -sv -b 4096 /dev/sdX 8191 0
```

Dernier bloc puis premier bloc, bornes incluses, en blocs de 4096 octets. Le disque choisi doit avoir au moins 32 Mio.

### 3. Garder les numéros dans le live en mémoire — jaune

```bash
sudo badblocks -sv -b 4096 -o /tmp/blocs-illisibles.txt /dev/sdX
```

Écrit seulement le rapport dans /tmp, en RAM ; le disque mesuré reste en lecture seule. Le rapport disparaît au redémarrage et ses unités dépendent de -b.

## Pièges

- -n réécrit des blocs et -w détruit les données : ne jamais les utiliser sur l’original à récupérer.
- Une surface lisible aujourd’hui ne garantit pas l’absence de panne intermittente.

## Voir aussi

`rescue-clone`, `rescue-smart`, guide 01.
