# @Input ⚒️

## Objectif :

Cet exercice vous permettra de vous familiariser avec la directive `@Input` en Angular. Vous allez créer une application simple qui affiche une liste d'articles. Chaque article sera affiché dans un composant enfant, et les données seront passées du composant parent au composant enfant à l'aide de la directive `@Input`.

## Contexte

Vous allez créer une application Angular avec deux composants : un composant parent qui gère une liste d'articles, et un composant enfant qui affiche les détails d'un article. Les données de chaque article seront transmises du parent à l'enfant via `@Input`.

1. Créer un Nouveau Projet Angular
2. Générez deux composants : `ArticleList` pour gérer la liste des articles (composant parent) et `ArticleItem` pour afficher chaque article individuellement (composant enfant)
3. Définir le Modèle de Données *
4. Utiliser `@Input` dans le Composant `ArticleItem`
5.  Afficher les Détails de l'Article dans `article-item.component.html`
6. Lier le Composant Parent et Enfant
7. Ajoutez un bouton "Afficher le détail" à chaque article. Lorsqu'il est cliqué, affichez ou masquez le contenu de l'article 

*Modèle de Données

```tsx
  articles: any[] = [
    { title: 'Angular Basics', content: 'Introduction to Angular...' },
    { title: 'Components and Templates', content: 'Understanding components...' },
    { title: 'Directives in Angular', content: 'How to use directives...' }
  ];
```

<aside>
💡 Pour faire cet exercice, aidez-vous du cours [*Input*](https://github.com/kerfiguetteb/cours-Angular/blob/main/Input.md)

</aside>