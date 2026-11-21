# rescue-lang — choisir la langue et le clavier

**Couleur : aucun.** Change les réglages de la session, pas les données des disques traités.

**Lancer :** menu SOS, rubrique Réglages → Langue et clavier ; ou dans un terminal : `rescue-lang`.

Dans les exemples, remplacer `sdX` et les chemins en majuscules après identification avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. Les outils qui en ont besoin demandent automatiquement les droits sudo.

## Usages

### 1. Voir langue et clavier actuels — aucun

```bash
rescue-lang --show
```

Affiche les réglages actuels sans relancer la session. Le choix du clavier est indépendant de la langue.

### 2. Lister les langues disponibles — aucun

```bash
rescue-lang --list
```

L’étoile marque la langue actuelle. Français et anglais sont les langues livrées.

### 3. Passer l’interface en anglais — aucun

```bash
rescue-lang --set en
```

Le menu et les Réglages changent immédiatement ; les autres applications après réouverture de session. Le choix est écrit dans `RESCUE-DATA/config/langue` si disponible en écriture, sinon gardé en mémoire.

### 4. Choisir un clavier français — aucun

```bash
rescue-lang --clavier fr
```

Applique une disposition française à la session graphique. Vérifier les touches dans un terminal avant de saisir une confirmation ou un mot de passe.

## Pièges

- Le choix `English` au démarrage passe avant le choix enregistré ; un choix de session reste prioritaire.
- Redémarrer la session ferme ses applications : sauvegarder les rapports avant `--redemarrer-session`.

## Voir aussi

`rescue-terminal-theme`, guide 13.
