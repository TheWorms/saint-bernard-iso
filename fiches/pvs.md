# pvs — inventorier les volumes physiques LVM

**Couleur : vert.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Partitions et volumes ; fenêtre `assistant-pvs` ; terminal : `sudo pvs`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est l’original protégé ; `sdY` une copie de travail distincte, démontée et sacrifiable. Ne jamais ouvrir l’original avec `rescue-rw`. Remplacer les chemins en majuscules après vérification. Les fichiers de `/tmp` sont en mémoire et disparaissent à l’arrêt.

## Usages

### 1. Relier PV et groupe de volumes — vert

```bash
sudo pvs -o pv_name,pv_uuid,vg_name,pv_size,pv_free
```

Lecture d’inventaire ; les membres manquants doivent être relevés avant une activation.

### 2. Afficher des tailles en octets — vert

```bash
sudo pvs --units b --nosuffix -o pv_name,pv_size,pv_free
```

Les octets permettent de comparer des capacités sans arrondis en Gio.

### 3. Produire un rapport JSON — vert

```bash
sudo pvs --reportformat json -o pv_name,pv_uuid,vg_name
```

Ne pas confondre l’UUID du PV avec celui du système de fichiers.

## Pièges

- Un PV n’est pas un système de fichiers ; ne pas le monter directement.
- pvs ne rend pas un LV actif. Ne pas improviser pvcreate, vgcfgrestore ou une activation en écriture sur les originaux.

## Voir aussi

`rescue-ro`, `rescue-rw`, `lsblk`, guide 08.
