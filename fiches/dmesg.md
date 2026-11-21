# dmesg — lire les messages du noyau

**Couleur : vert.** Lecture du tampon noyau ; aucune remise à zéro des messages.

**Lancer :** menu SOS, rubrique Diagnostic des disques ; fenêtre `assistant-dmesg` ; terminal : `sudo dmesg`.

Identifier les disques avec `lsblk -o NAME,SIZE,MODEL,SERIAL` avant de remplacer `sdX`, `sdY` ou `nvme0`. Les lectures intensives se font sur une copie ou un support sain. Ne jamais ouvrir l’original à récupérer avec `rescue-rw`.

## Usages

### 1. Lire les messages avec leur date estimée — vert

```bash
sudo dmesg --ctime
```

Rechercher erreurs d’E/S, resets et déconnexions. Les dates reconstruites peuvent être trompeuses après une suspension ou un changement d’horloge.

### 2. Isoler avertissements et erreurs — vert

```bash
sudo dmesg --ctime --level=err,warn
```

Une sortie vide signifie seulement que ces niveaux sont absents du tampon courant ; les anciens messages peuvent avoir été écrasés.

### 3. Suivre les nouvelles erreurs pendant une lecture — vert

```bash
sudo dmesg --follow --human
```

Laisser ce terminal ouvert pendant la lecture de la copie. Ctrl+C arrête le suivi, pas la commande de copie dans un autre terminal.

## Pièges

- Ne pas utiliser --clear ou --read-clear avant de conserver les indices.
- Un refus d’accès sous rescue demande sudo, pas un changement global des protections du noyau.

## Voir aussi

`rescue-hwinfo`, `rescue-collect`, guide 01.
