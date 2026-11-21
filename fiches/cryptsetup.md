# cryptsetup — examiner et ouvrir LUKS sans écriture

**Couleur : vert.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Partitions et volumes ; fenêtre `assistant-cryptsetup` ; terminal : `sudo cryptsetup`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une copie de travail distincte, démontée et sacrifiable. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. Les fichiers de `/tmp` sont en mémoire et disparaissent à l’arrêt.

## Usages

### 1. Lire l’en-tête LUKS — vert

```bash
sudo cryptsetup luksDump /dev/sdX1
```

Affiche version, UUID et emplacements de clés, sans déchiffrer les fichiers.

### 2. Ouvrir le conteneur en lecture seule — vert

```bash
sudo cryptsetup open --readonly /dev/sdX1 recup_luks
```

Saisir la phrase au terminal. Avec une clé fichier autorisée, ajouter --key-file /CHEMIN/cle. Le système de fichiers dans /dev/mapper/recup_luks doit lui aussi être monté en lecture seule.

### 3. Refermer son propre conteneur — vert

```bash
sudo cryptsetup close recup_luks
```

Démonter d’abord tous ses points de montage et sortir les terminaux de ces dossiers. Ne fermer que le nom ouvert pendant cette intervention.

## Pièges

- luksFormat efface l’accès aux données : ne jamais le lancer pour ouvrir un volume existant.
- Ne pas mettre un vrai secret dans une commande, un rapport ou une capture ; préserver l’en-tête LUKS.

## Voir aussi

`rescue-ro`, `rescue-rw`, `lsblk`, guide 08.
