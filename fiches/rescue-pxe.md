# rescue-pxe — servir Saint-Bernard par le réseau

**Couleur : orange.** Active un service réseau arrêté par défaut ; n’écrit pas les disques traités.

**Lancer :** menu SOS, rubrique Réseau ; ou dans un terminal : `rescue-pxe`.

Dans les exemples, remplacer `sdX` et les chemins en majuscules après identification avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. Les outils qui en ont besoin demandent automatiquement les droits sudo.

## Usages

### 1. Consulter l’état — vert

```bash
rescue-pxe etat
```

Affiche le mode, l’adresse et les PC servis si le service est actif. Ne démarre aucun serveur.

### 2. Servir sur un réseau avec DHCP existant — orange

```bash
rescue-pxe on --interface INTERFACE
```

Démarre le proxy DHCP sur la carte choisie ; ne modifie aucun disque, donc aucune cible disque à ouvrir. Vérifier le nom avec `ip -br link` et l’accord pour servir ce réseau ; la box conserve l’attribution des adresses.

### 3. Servir sur un câble direct isolé — orange

```bash
rescue-pxe on --isole --interface INTERFACE
```

Attribue `10.77.77.1` à cette carte et distribue des adresses : uniquement sur un réseau isolé sans autre DHCP. Ne touche aucun disque ; vérifier physiquement le câble et la carte avec `ip -br link` pour ne pas agir sur le mauvais réseau.

### 4. Arrêter et restaurer la carte — vert

```bash
rescue-pxe off
```

Arrête les services et remet la carte dans son état précédent. Les clients ont besoin d’au moins 3 Gio de RAM pour charger le système.

## Pièges

- Ne jamais employer `--isole` sur le réseau de la box.
- Les fichiers système viennent du support live ; une VM sans ce support ne peut pas valider le démarrage des clients.

## Voir aussi

`rescue-net`, `rescue-ssh`, guide 13.
