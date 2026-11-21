# rescue-ssh — ouvrir temporairement un accès distant

**Couleur : orange.** L’accès distant donne au compte rescue les droits sudo.

**Lancer :** menu SOS, rubrique Réseau ; Réglages → Réseau et partage ; ou dans un terminal : `rescue-ssh`.

Dans les exemples, remplacer `sdX` et les chemins en majuscules après identification avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. Les outils qui en ont besoin demandent automatiquement les droits sudo.

## Usages

### 1. Vérifier l’état sans ouvrir d’accès — vert

```bash
rescue-ssh etat
```

Affiche l’état, les adresses et les empreintes si actif. Aucun mot de passe ne doit être copié dans un rapport partagé.

### 2. Activer sur un réseau de confiance — orange

```bash
rescue-ssh on
```

Crée les clés et change le mot de passe du compte rescue ; ne choisit ni n’écrit de disque de récupération. Vérifier le réseau et l’empreinte affichée avec le correspondant : l’accès sudo permettrait ensuite d’écrire n’importe quel disque après ouverture par `rescue-rw` et contrôle de son modèle et de sa série.

### 3. Fermer l’accès et les sessions — vert

```bash
rescue-ssh off
```

Arrête le serveur, ferme les sessions SSH et remet l’ancien mot de passe. À faire dès la fin de l’assistance.

## Pièges

- Désactivé au démarrage ; ne pas l’activer sur un réseau public.
- Les clés d’hôte changent au redémarrage : comparer les empreintes, ne pas supprimer aveuglément une alerte du client SSH.

## Voir aussi

`rescue-net`, `rescue-pxe`, guide 13.
