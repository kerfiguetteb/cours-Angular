# introduction

💡 [documentation](https://angular.fr/)

# ⚒️ Prérequis:

Pour appréhender sereinement Angular, il faut être un minimum à l'aise avec les sujets suivants :

- HTML/CSS
- JavaScript
- TypeScript

# Introduction:

## Présentation

- Angular est un framework créé en 2009 (Angular JS)
- Il a révolutionné le dev web à son époque

## Fonctionnalités

- Des éléments qui s'exécutent côté client et non côté serveur
- Une navigation sans rafraîchissement (SPA*)

> Une **SPA (Single Page Application)**, ou application monopage, est une application web qui fonctionne sur une seule page web. Contrairement aux sites traditionnels où chaque action de l'utilisateur entraîne le chargement d'une nouvelle page, une SPA charge une seule page au début, puis met à jour dynamiquement le contenu en fonction des interactions de l'utilisateur. Cela permet une navigation plus fluide et rapide, car il n'y a pas besoin de recharger entièrement la page à chaque fois. Le contenu est souvent mis à jour en utilisant JavaScript, sans que la page entière ne soit rechargée.
> 

## Fonctionnement

- Fonctionne avec des composants
- Ils sont comme un ensemble de briques pour constituer notre application
- Les composants sont indépendants, génériques et réutilisables
- Une page est donc un agglomérat de composants

## TypeScript

- Depuis sa reprise par ***Google***, Angular a entièrement été redéveloppé en TypeScript
- Il est possible de développer des sites Angular en JS, mais c'est fortement déconseillé
- En effet, contrairement à JS, le TS est vérifié à la compilation

## La manipulation du DOM

- Le DOM est un élément central des sites traditionnels
- On manipule le DOM grâce à du JavaScript notamment
- Il nous permet d'interagir dynamiquement avec le HTML via des scripts plutôt qu'en dur

## Le DOM Virtuel

- La librairie React a introduit la notion de DOM virtuel
- Angular se base entièrement sur ce concept
- Consiste à avoir une représentation en mémoire du DOM
- Toute modification sera effectuée sur le DOM virtuel (en local donc), puis sera envoyée au DOM physique

```tsx
ng new MaPremiereApp
cd ./MaPremiereApp
ng serve -o
```