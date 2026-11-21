# sha256sum — calculer et vérifier des empreintes

**Couleur : vert.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Clonage et images ; fenêtre `assistant-sha256sum` ; terminal : `sha256sum`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est la source protégée ; `sdY` une destination distincte. Pour l’analyse, préférer une copie ; ne jamais ouvrir l’original à récupérer avec `rescue-rw`. Les chemins en majuscules sont à remplacer après vérification.

## Usages

### 1. Calculer l’empreinte d’une image — vert

```bash
sha256sum /mnt/COPIE/disque.img
```

Lit toute l’image ; comparer les 64 caractères hexadécimaux, pas seulement le nom du fichier.

### 2. Créer un manifeste relatif dans le live — vert

```bash
cd /mnt/COPIE &&
sha256sum disque.img > /tmp/disque.sha256
```

Le manifeste est en RAM. Le nom relatif permet de vérifier depuis un autre dossier contenant la même image ; copier ensuite le manifeste sur une destination autorisée.

### 3. Vérifier une image contre le manifeste — vert

```bash
cd /mnt/COPIE &&
sha256sum --check /tmp/disque.sha256
```

Un code non nul est un échec de vérification ou d’accès ; une empreinte égale ne certifie pas que l’image initiale était complète.

## Pièges

- Conserver la provenance et la date du manifeste.
- Hacher un disque fragile le relit entièrement : cloner d’abord.

## Voir aussi

`ddrescue`, `pv`, guide 04.
