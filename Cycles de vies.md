# Cycles de vies

## Les États

Les différents états d’un composant:

- `constructor` : lorsque le composant est créé
- `ngOnChanges()`: lorsque le composant est modifié
- `ngOnInit()` : lorsque le composant est affiché
- `ngDoCheck()` : Permet de définir une détection de changement personnalisée
- `ngOnDestroy()` :lorsque le composant est détruit

### `Constructeur`

- Partie qui concerne la création du composant
- C’est ici que les dépendances son injectées

### `ngOnChanges()`

- `ngOnChanges()` est le premier à être appelé
- Elle est notamment liée aux `@Inputs()` de l'objet
- A chaque fois que l'objet est modifié, `ngOnChanges()` est appelé
- Il nous permet aussi de récupérer l'historique de ces modifications

### `ngDoCheck()`

- `ngDoCheck()` est appelée après chaque détection de changement par `ngOnChanges()`
- Elle est aussi appelée juste après `ngOnInit()` lors de la première initialisation.
- Elle permet d'agir sur les changements qu'Angular ne peut pas détecter lui même.

### `ngOnDestroy()`

- Est appelée en dernier
- S’exécute juste avant que le composant soit détruit (déchargé)
- elle sert notamment à fermer les souscriptions des événements

## LIFECYCLE HOOKS

- Ces méthodes s’appellent des hooks de cycle de vie
- Il en existe d’autre plus avancés, comme `ngAfterViewInit` et `ngAfterViewChecked`

## LES DIRECTIVES

- Vous avez déjà utilisé des directives à plusieurs reprises
- Notamment les `@if` et `@for`
- Il en existe toutefois d’autre

## DEUX TYPES

On distingues 2 types de directives:

- **Les directives d’attributs** : Elles modifient l'apparence ou le comportement d'un élément existant.
- **Les directives structurelles** : Elles modifient la structure du DOM en ajoutant ou supprimant des éléments.

### Les directives d’attributs

- `ngClass` : Permet d’ajouter ou supprimer des classes sur un élément
- `ngStyle` : Permet de modifier les styles d’un élément
- `ngModel` : Two Way Binding sur un élément HTML

### Les directives structurelles

- `@if` : Permet de définir une condition pour afficher ou non un élément
- `@for`: permet de créer une boucle sur une liste d'éléments et de répéter un bloc HTML pour chaque élément.
- `@switch`: Permet de basculer entre plusieurs templates en fonction de la valeur d'une expression.

## DIRECTIVE AVANCÉE

- Tout comme les pipes, il est possible de créer des directives personnalisées!
- C’est toutefois un pratique complexe et avancée.