# testdisk — analyser une copie et ses partitions

**Couleur : rouge.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Récupération de fichiers ; fenêtre `assistant-testdisk` ; terminal : `sudo testdisk`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est la source protégée ; `sdY` une destination distincte. Pour l’analyse, préférer une copie ; ne jamais ouvrir l’original à récupérer avec `rescue-rw`. Les chemins en majuscules sont à remplacer après vérification.

## Usages

### 1. Lister la table sans écrire — vert

```bash
sudo testdisk /list /dev/sdX
```

Affiche la structure détectée ; cela ne répare rien. Une taille plausible n’est pas une preuve que la table est correcte.

### 2. Analyser une image en gardant le journal en RAM — jaune

```bash
cd /tmp &&
sudo testdisk /log /mnt/COPIE/disque.img
```

Choisir Analyse puis les recherches adaptées ; lire les fichiers avec P si possible. Ne pas valider Write pendant cette analyse.

### 3. Réécrire une table sur une copie sacrifiable — rouge

```bash
rescue-rw /dev/sdY &&
cd /tmp &&
sudo testdisk /log /dev/sdY
```

Écrit la table seulement après Write dans l’interface. sdY doit être une copie sacrifiable, distincte de l’original ; vérifier modèle, série et bornes avant confirmation.

## Pièges

- Ne pas écrire une table proposée avant d’avoir recoupé tailles, systèmes de fichiers et contenu.
- Une recherche approfondie peut solliciter tout le disque ; cloner un original fragile avant.

## Voir aussi

`mmls`, `photorec`, guide 06.
