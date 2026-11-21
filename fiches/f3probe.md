# f3probe — sonder une capacité flash sur un support sacrifiable

**Couleur : rouge.** La sonde écrit des blocs bruts, même lorsqu’elle tente de les restaurer.

**Lancer :** menu SOS, rubrique Tests et mesures ; fenêtre `assistant-f3probe` ; terminal : `sudo f3probe`.

Identifier les disques avec `lsblk -o NAME,SIZE,MODEL,SERIAL` avant de remplacer `sdX`, `sdY` ou `nvme0`. Les lectures intensives se font sur une copie ou un support sain. Ne jamais ouvrir l’original à récupérer avec `rescue-rw`.

## Usages

### 1. Lire les modes avant de brancher la cible — vert

```bash
sudo f3probe --help
```

Lire les options de la version installée. Cela n’attache aucun support et n’écrit rien.

### 2. Sonder en restaurant les blocs à la fin — rouge

```bash
rescue-rw /dev/sdY
sudo f3probe --min-memory --reset-type=2 --time-ops /dev/sdY
```

sdY est un support sacrifiable, identifié par modèle, taille et série, démonté et distinct de l’original. Retaper le nom demandé par rescue-rw. Une interruption peut empêcher la restauration : sauvegarder d’abord tout ce qui compte.

### 3. Sonder sans restaurer les blocs — rouge

```bash
rescue-rw /dev/sdY
sudo f3probe --min-memory --reset-type=2 --destructive --time-ops /dev/sdY
```

Écrit sur le support entier sdY et laisse les blocs modifiés ; seulement une cible de test entièrement sacrifiable. Après démontage et intervention, refermer avec rescue-ro /dev/sdY. Une capacité plausible dans QEMU ne valide pas une vraie clé USB.

## Pièges

- Ne jamais choisir la source à récupérer ni un disque contenant une copie encore utile.
- Arrêter un processus ne rétablit pas nécessairement les données déjà écrites ; ne pas promettre une restauration après coupure.

## Voir aussi

`f3read`, `f3write`, `rescue-ro`, guide 01.
