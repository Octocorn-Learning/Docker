# Conseils de rédaction

## Structure

```bash
root
|   index.md # Table des matières
|   exercices # Répertoire contenant les exercices
|   |   01_exercice # Répertoire contenant l'exercice 01
|   |   |   01_exercice.poussin.md 
|   |   |   01_exercice.poulet.md
|   |   |   01_exercice.coq.md
|   cours # Répertoire contenant les cours
|   |   01_cours.slides.md # Cours 01
```

## Nomenclature

> ⚠️ Chaque nouveau chapitre doit être ajouté à la table des matières (`index.md`) ⚠️

### Cours

- Les fichiers sont placés dans le répertoire `./cours`
- Ils sont suffixés par `.slides.md`

### Exercices

- Les fichiers sont placés dans le répertoire `./exercices`
- On compte un répertoire par exercice
- Le niveau de difficulté (poussin, poulet ou coq) de l'exercice est précisé en suffixe : `01_exercice.poussin.md`

### Corrections et démonstrations

- Les corrections et démonstrations sont placées dans le répertoire `./espace formateur`
- Il s'agit d'un submodue git pointant vers un autre dépôt privé contenant des : 
    - corrections
    - démonstrations
    - ressources