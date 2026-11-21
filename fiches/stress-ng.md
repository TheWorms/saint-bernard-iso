# stress-ng — charger CPU et mémoire avec une durée fixée

**Couleur : jaune.** Les exemples ne lancent aucun stress disque ou réseau.

**Lancer :** menu SOS, rubrique Tests et mesures ; fenêtre `assistant-stress-ng` ; terminal : `stress-ng`.

Identifier les disques avec `lsblk -o NAME,SIZE,MODEL,SERIAL` avant de remplacer `sdX`, `sdY` ou `nvme0`. Les lectures intensives se font sur une copie ou un support sain. Ne jamais ouvrir l’original à récupérer avec `rescue-rw`.

## Usages

### 1. Charger une tâche CPU pendant 20 secondes — jaune

```bash
stress-ng --cpu 1 --timeout 20s --metrics-brief --verify
```

Fermer les autres logiciels et surveiller température et stabilité. Le retour zéro ne garantit pas un matériel sain.

### 2. Charger 128 Mio de mémoire pendant 20 secondes — jaune

```bash
stress-ng --vm 1 --vm-bytes 128M --vm-keep --timeout 20s --metrics-brief --verify
```

Une seule tâche : les 128 Mio ne sont pas multipliés. Conserver une marge pour le live ; aucun swap n’est activé et une allocation excessive peut faire tuer des processus.

### 3. Vérifier une méthode de calcul déterminée — jaune

```bash
stress-ng --cpu 1 --cpu-method fft --timeout 20s --metrics-brief --verify
```

Conserver la même méthode pour comparer deux essais. Un échec peut venir du processeur, de la mémoire, de l’alimentation ou du refroidissement.

## Pièges

- Le délai termine la charge ; un arrêt forcé ou un dépassement n’est pas un essai réussi.
- Ne pas recopier une commande --hdd sur le disque à récupérer ; les tests d’écriture demandent une destination saine et rescue-rw.

## Voir aussi

`memtester`, `sensors`, guides 01 et 02.
