# tune2fs — lire ou modifier les paramètres ext sur une copie

**Couleur : rouge.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Systèmes de fichiers ; fenêtre `assistant-tune2fs` ; terminal : `sudo tune2fs`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une copie de travail distincte, démontée et sacrifiable. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. Les fichiers de `/tmp` sont en mémoire et disparaissent à l’arrêt.

## Usages

### 1. Lister les paramètres sans écriture — vert

```bash
sudo tune2fs -l /dev/sdX1
```

Lire UUID, compteur de montages et fonctions avant toute modification.

### 2. Étiqueter une copie de travail — orange

```bash
rescue-rw /dev/sdY &&
sudo tune2fs -L COPIE-TEST /dev/sdY1
```

Écrit le superbloc de la copie ext démontée, jamais celui de l’original.

### 3. Donner un nouvel UUID à une copie — orange

```bash
rescue-rw /dev/sdY &&
sudo tune2fs -U random /dev/sdY1
```

Copie ext démontée : évite deux UUID identiques après clonage. Mettre à jour ses références fstab et démarrage si cette copie doit démarrer.

## Pièges

- Changer UUID ou étiquette peut casser fstab, les montages et le démarrage.
- Ne pas désactiver journal, fonctions ou contrôles périodiques pour contourner une panne.

## Voir aussi

`rescue-ro`, `rescue-rw`, `ddrescue`, guide 09.
