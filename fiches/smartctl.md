# smartctl — lire SMART et les autotests

**Couleur : vert.** Les lectures de rapport sont vertes ; lancer un autotest sollicite le disque.

**Lancer :** menu SOS, rubrique Diagnostic des disques ; fenêtre `assistant-smartctl` ; terminal : `sudo smartctl`.

Identifier les disques avec `lsblk -o NAME,SIZE,MODEL,SERIAL` avant de remplacer `sdX`, `sdY` ou `nvme0`. Les lectures intensives se font sur une copie ou un support sain. Ne jamais ouvrir l’original à récupérer avec `rescue-rw`.

## Usages

### 1. Lire le rapport courant — vert

```bash
sudo smartctl -a /dev/sdX
```

Contrôler modèle et série avant la lecture. Un statut PASSED ne garantit pas un disque sain ; smartctl renvoie un masque de bits, pas seulement 0 ou 1.

### 2. Lire les journaux étendus — vert

```bash
sudo smartctl -x /dev/sdX
```

Regroupe identité, attributs, erreurs et historique disponibles. Si le pont USB bloque SMART, suivre le guide 01 ; ne pas essayer au hasard des réglages du contrôleur.

### 3. Démarrer un autotest court sur un disque stable — jaune

```bash
sudo smartctl -t short /dev/sdX
```

Sur un disque fragile, cloner avant ce test. La commande lance le test interne puis rend la main ; respecter le délai indiqué avant de lire le résultat.

### 4. Relire le résultat de l’autotest — vert

```bash
sudo smartctl -l selftest /dev/sdX
```

À lancer après le délai annoncé. Un test interrompu ou non pris en charge ne doit pas être présenté comme réussi.

### 5. Retrouver les options du contrôleur — vert

```bash
sudo smartctl --help
```

Consulter les types de transport et les options de rapport de la version installée, sans modifier le disque.

## Pièges

- Ne pas confondre lecture seule du noyau et protection contre les commandes internes du contrôleur.
- Les bits du code de retour distinguent problème de commande, alerte de santé et erreurs historiques ; lire le rapport.

## Voir aussi

`rescue-smart`, `rescue-clone`, guide 01.
