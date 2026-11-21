# ddrescuelog — examiner une carte ddrescue

**Couleur : vert.** Les usages ci-dessous précisent leur risque propre.

**Lancer :** menu SOS, rubrique Clonage et images ; fenêtre `assistant-ddrescuelog` ; terminal : `ddrescuelog`.

Identifier modèle, série et taille avec `lsblk -o NAME,SIZE,MODEL,SERIAL`. `sdX` est la source protégée ; `sdY` une destination distincte. Pour l’analyse, préférer une copie ; ne jamais ouvrir l’original à récupérer avec `rescue-rw`. Les chemins en majuscules sont à remplacer après vérification.

## Usages

### 1. Afficher le bilan de la carte — vert

```bash
ddrescuelog -t /mnt/DESTINATION/TRAVAIL/disque.map
```

Distinguer terminé, non essayé et secteurs en erreur ; travailler sur la carte correspondant à cette image. Utiliser sudo si ses permissions l’exigent.

### 2. Tester si la récupération est complète — vert

```bash
ddrescuelog -D /mnt/DESTINATION/TRAVAIL/disque.map
```

Code 0 : toutes les zones de cette carte sont terminées ; ce n’est pas une validation du système de fichiers. Un code non nul demande de lire le bilan.

### 3. Lister les blocs récupérés de 4096 octets — vert

```bash
ddrescuelog -b4096 -l+ /mnt/DESTINATION/TRAVAIL/disque.map > /tmp/blocs-recuperes.txt
```

Écrit seulement une liste en RAM. Les unités de -b doivent être conservées ; ne pas transmettre cette liste comme une liste de blocs défectueux.

## Pièges

- Ne pas confondre les types + (récupéré) et - (défectueux).
- Ne pas modifier la carte maître pour fabriquer un bilan rassurant.

## Voir aussi

`ddrescue`, guide 04.
