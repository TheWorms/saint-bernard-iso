# ioping — mesurer la latence de lecture

**Couleur : jaune.** Lecture intensive sur un périphérique ; ne pas passer un dossier à sa place.

**Lancer :** menu SOS, rubrique Tests et mesures ; fenêtre `assistant-ioping` ; terminal : `sudo ioping`.

Identifier les disques avec `lsblk -o NAME,SIZE,MODEL,SERIAL` avant de remplacer `sdX`, `sdY` ou `nvme0`. Les lectures intensives se font sur une copie ou un support sain. Ne jamais ouvrir l’original à récupérer avec `rescue-rw`.

## Usages

### 1. Mesurer dix lectures sans cache — jaune

```bash
sudo ioping -c 10 -i 0.2 -D /dev/sdX
```

Choisir une copie ou un disque stable. Le mode direct écarte le cache Linux, pas tous les caches du contrôleur.

### 2. Mesurer les accès rapides pendant trois secondes — jaune

```bash
sudo ioping -R /dev/sdX
```

Ce mode mesure les accès de lecture par seconde. Les temps d’un disque virtuel ne sont pas une recette matérielle.

### 3. Comparer avec des lectures de 1 Mio — jaune

```bash
sudo ioping -c 5 -i 0.2 -D -s 1M /dev/sdX
```

Comparer à conditions identiques et sans autre charge. Ne pas ajouter -W ou -G : ces modes peuvent écrire.

## Pièges

- Sur un dossier, ioping crée un fichier de travail : ce n’est pas la lecture seule du périphérique.
- Un échec d’accès direct doit être compris, pas converti en succès ; cloner d’abord un disque instable.

## Voir aussi

`rescue-bench`, `hdparm`, guide 01.
