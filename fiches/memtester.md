# memtester — tester une allocation de RAM

**Couleur : vert.** Teste la mémoire allouée sans écrire sur les disques ; la charge peut être importante.

**Lancer :** menu SOS, rubrique Mémoire (RAM) ; fenêtre `assistant-memtester` ; terminal : `sudo memtester`.

Identifier les disques avec `lsblk -o NAME,SIZE,MODEL,SERIAL` avant de remplacer `sdX`, `sdY` ou `nvme0`. Les lectures intensives se font sur une copie ou un support sain. Ne jamais ouvrir l’original à récupérer avec `rescue-rw`.

## Usages

### 1. Faire une boucle sur 128 Mio — vert

```bash
sudo memtester 128M 1
```

Vérifier auparavant la mémoire disponible avec free -m et laisser une marge pour le live. Cette quantité prudente illustre la commande ; elle ne teste pas la RAM occupée par le système.

### 2. Répéter trois boucles sur 64 Mio — vert

```bash
sudo memtester 64M 3
```

À utiliser si la première boucle est propre mais la panne intermittente. La durée dépend du matériel ; le code combine 1 allocation/verrouillage, 2 adresses bloquées et 4 autres tests.

### 3. Lire la syntaxe sans allouer — vert

```bash
sudo memtester
```

Sans taille, affiche la syntaxe et renvoie une erreur d’usage, sans lancer de test. Toujours indiquer un nombre de boucles pour éviter le fonctionnement indéfini.

## Pièges

- Ne pas utiliser -p sur /dev/mem pour tester la mémoire de cette machine.
- Une réussite n’exclut pas un défaut intermittent ; une erreur ne désigne pas à elle seule la barrette fautive.

## Voir aussi

`stress-ng`, `edac-util`, guide 02.
