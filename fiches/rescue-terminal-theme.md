# rescue-terminal-theme — choisir les couleurs du terminal

**Couleur : aucun.** Règle LXTerminal sans toucher aux disques traités.

**Lancer :** menu SOS, rubrique Réglages → Texte et terminal ; ou dans un terminal : `rescue-terminal-theme`.

Dans les exemples, remplacer `sdX` et les chemins en majuscules après identification avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. Les outils qui en ont besoin demandent automatiquement les droits sudo.

## Usages

### 1. Lister les jeux disponibles — aucun

```bash
rescue-terminal-theme --list
```

L’étoile marque le jeu actuel ; utiliser le nom court pour le sélectionner.

### 2. Appliquer le jeu Saint-Bernard — aucun

```bash
rescue-terminal-theme --set saint-bernard
```

Écrit la configuration du terminal de la session et, si disponible en écriture, `RESCUE-DATA/config`. Le changement est visible dans les nouveaux terminaux.

### 3. Voir les messages de démonstration — aucun

```bash
rescue-terminal-theme --show
```

Affiche des exemples d’états et d’avertissements. Les mots et marqueurs restent nécessaires, même avec un jeu monochrome.

### 4. Vérifier contraste et couleurs de sécurité — aucun

```bash
rescue-terminal-theme --verifier
```

Contrôle chaque jeu sans modifier les réglages. Une lecture visuelle sur l’écran cible complète ce contrôle.

## Pièges

- Les terminaux déjà ouverts ne reprennent le thème qu’à leur prochain lancement.
- Sans `RESCUE-DATA` en écriture, le choix reste en mémoire et sera perdu à l’extinction.

## Voir aussi

`rescue-lang`, guide 13.
