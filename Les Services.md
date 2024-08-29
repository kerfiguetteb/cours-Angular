# Les Services

- Un service à pour but de contenir toute la logique fonctionnelle et/ou technique
- Il est régulièrement utiliser pour communiquer avec une API
- Il sera consommé par un composant, qui l'appellera pour récupérer les données sans avoir à se soucier de leur obtention

## SINGLE RESPONSIBILITY

- Le principe de responsabilité unique est très important en développement
- Il implique que chaque objet n'ait QU'UNE seule responsabilité dans le programme
- Par exemple, un composant ne doit servir qu'à afficher les data, pas à les récupérer

## STATELESS

- Un composant qui ne stock pas de data est dit **stateless**
- Dans le cas inverse, on parle de composant **stateful**

## Préparer notre environnement

- Avant de pouvoir monter un service pour récupérer des data sur une API, il faut une API!!
- Nous allons donc utiliser `JSON-SERVER` comme API pour ce projet

## JSON SERVER

### API

- API: **A**pplication **P**rogramming **I**nterface
- C’est une solution qui permet à des applications de communiquer via des requêtes HTTP (GET,POST,PUT,DELETE)

### JSON SERVER

- JSON-Server est un serveur `Node.js` qui permet de gérer des données
- Il permet de  créer un serveur qui va gérer des données `JSON`
- On pourra très facilement créer une API à partir d’un fichier `JSON`

### AVANTAGES/INCONVENIENTS

- Il est pratique et facile à utiliser pour un projet de développement
- En revanche, c’est impensable de s’en servir en production!

### INSTALLATION

- A la racine du projet, créez un répertoire nommé "db”
- Ajoutez y un fichier nommé `data.json` et ajoutez y les data contenues dans `products page.component.ts`
- Tapez la commande `npm i --save-dev json-server`
- Dans le fichier `package.json`, ajoutez la ligne suivante dans la section scripts:

```tsx
  "scripts": {
    //
    "api": "json-server --watch db/data.json"
  },

```

- l’installation est terminée, pour démarrer le serveur : `npm run api`

## MODÈLE DE DONNÉES

- Un modèle de données est une classe ou interface qui représente un objet
- Il permet de garantir l'uniformité des données entrantes et sortantes
- En outre, on pourra manipuler nos objets comme types et arrêter d'utiliser any !

### DECLARER UN MODÈLE

- Nous devons d'abord créer un répertoire `src/app/models`
- Nous devons ensuite créer un chier `nomModel.model.ts`
- Le suffixe `.model.ts` est une bonne pratique pour identifier un fichier comme un modèle

### DEUX TYPES DE MODÈLES

- Nous pouvons nous baser sur des classes ou des interfaces
- Les interfaces sont utiles si on a juste besoin de définir un contrat entre nos données et le modèle
- Les classes seront utilisés surtout si on a besoin de faire des instances
- On pourra faire de la vérification de type dans tous les cas.

### Pourquoi une classe?

- Doit être préféré uniquement si l’app a besoin d’instances lors de la mise en prod
- Également, les classes perdureront lors de la prod, contrairement aux interfaces

### Pourquoi une Interface?

- Sera préférable si on a juste besoin de vérifier le contrat entre les données et l'interface
- Pour rappel, un contrat est un ensemble de conditions qui doit être respectées par la donnée

### Exemple

- Ici, nous allons partir sur des interfaces.
- En effet, nous n’avons pas besoin de créer des instances
- Nous allons juste vérifier que les données sont conformes au contrat

### Interfaces à créer

- Nous avons deux types de données: `films` et `albums`
- Les deux ont des propriétés communes: `id,nom,annee,img`
- Nous allons créer une interface générique, puis une interface pour chaque type de données

### `product.model.ts`

```tsx
 export default interface Product {
 id: number;
 nom: string;
 annee: number;
 img: string;
 details: string;
 }
```

### `film.model.ts`

```tsx
 // Import de l'interface Product
 import Product from "./product.model";
 
 // Création du modèle Film qui est une interface qui étend Product
 export default interface Film extends Product {
	 real: string;
	 synopsis: string;
 }
```

### `album.model.ts`

```tsx
 import Product from "./product.model";
 
 export default interface Album extends Product {
	 artiste: string;
 }
```

## CRÉER UN SERVICE

- Pour créer un service, on utilise la commande suivante:

```tsx
ng generate service nomService
```

ou

```tsx
ng g s nomService
```

## HTTPCLIENTMODULE

- `HttpClientModule` est un module qui permet de faire des requêtes HTTP
- Nous allons l’intégrer dans notre service
- Nous devons l’importer dans nos services

### Pourquoi faire?

- le module `HttpClientModule` permet de faire des requêtes **CRUD**
- C’est grâce à lui que nous allons notamment pouvoir faire des requêtes GET, POST PUT, DELETE
- Ce module devra être injecté en tant que **dépendance** dans le constructeur de notre service

## LES OBSERVABLES

- `HttpClientModule`va nous permettre de récupérer les données et de créer un objet `Observable`
- Un `Observable` est un objet qui sera observé par notre composant
- Le composant va **s'abonner** à l'`Observable` et va récupérer les données quand elles seront
disponibles/modifiées

### Analogie

- On peut imaginer l’observable comme étant une **newsletter**
- Des personnes souscrivent à cette newsletter
- Ils sont notifiées quand une nouvelle publication est disponible
- ils sont donc toujours au courant des nouveautés !

### En résumé

- **Le service:** aura un observable pour chaque requête HTTP (GET,POST,PUT,DELETE)
- **Le composant :** va ‘`subscribe` (s’abonner) aux `Observable` de son choix

### Créer notre service

- Nous allons créer un répertoire `services` dans `src\app`
- Nous allons ensuite créer deux services :
    - `ng g s services/film`
    - `ng g s services/album`
- Les fichiers `film.service.ts` et `album.service.ts` sont créés automatiquement et sont préremplis

### Le fichier `xx.service.ts`

Le ficher créé est prérempli avec les import et les déclaration suivantes

```tsx
 // Import du décorateur Injectable
 import { Injectable } from '@angular/core';

 // Appel du décorateur Injectable qui permet de créer les données lorsque le service sera injecté 
 
 @Injectable({ 
  providedIn: 'root' 
 }) 
 export class ProductService { 
 // On codera ici les différentes routes de notre service 10
 }
```

### Exemple

Créons un service pour chaque type de données

- Nous créons nos services pour les films et les albums
- Grâce à eux, nous allons pouvoir gérer les données des films et albums

Dans `film.service.ts`

```tsx
// import du décorateur Injectable
import { HttpClient } from '@angular/common/http';
import { Injectable } from '@angular/core';
import { Observable } from 'rxjs';
import Film from '../models/film.model';

// Appel du décorateur Injectable qui permet de créer les données lorsque le service sera injecté
@Injectable({
  providedIn: 'root'
})
export class FilmService {

  // Déclaration de l'URL vers notre API, pour ne pas avoir à la rappeller à chaque fois.
  // Idéalement, on devrait la placer en tant que variable d'environnement. On verra ça plus tard
  private apiUrl = 'http://localhost:3000';

  // Injection de la dépendence HttpClient
  constructor(private httpClient: HttpClient) { }

    // Création des différentes routes vers mon API
  // On déclare le type del'observable comme étant un tableau de film
  getFilms(): Observable<Film[]> {
    // On demande à retourner une liste de films (Film étant notre interface)
    // La partie entre parenthèse correspond à l'URL complète de notre route API
    return this.httpClient.get<Film[]>(`${this.apiUrl}/films`)
  }

  // Idem ici mais pour récupérer un film en particulier
  // Lorsqu'on appellera la méthode, on devra alors lui passer l'ID en argument
  getFilm(id: number): Observable<Film> {
    return this.httpClient.get<Film>(`${this.apiUrl}/films/${id}`);
  }

  createFilm(film: Film): Observable<Film> {
    return this.httpClient.post<Film>(`${this.apiUrl}/films`, film);
  }
  // attention au paramètre de l'URL ${film.id} 
  // celui-ci fait référence au paramètre de l'objet film déclaré comme argument de ma fonction 
  updateFilm(film: Film): Observable<Film> {
    return this.httpClient.put<Film>(`${this.apiUrl}/films/${film.id}`, film);
  }

  deleteFilm(id: number): Observable<Film> {
    return this.httpClient.delete<Film>(`${this.apiUrl}/films/${id}`);
  }

}
```

## UTILISER UN SERVICE

- Nous souhaitons maintenant appeler un service pour récupérer les données
- Nous allons créer la souscription dans notre composant
- Le but étant de souscrire à l’observable généré par notre service.

Deux étapes pour souscrire:

1. Ajouter le service comme dépendance, dans le constructeur
2. Appeler la méthode souhaitée du service et y souscrire, dans `ngOnInit()`

```tsx
 import { Component, OnInit } from '@angular/core'; 1
 
 // Import du service à utiliser 4
 import { NomService } from 'src/app/services/film.service'; 
 
 @Component({ 7
  selector: 'app-products-page', 
  templateUrl: './products-page.component.html', 
  styleUrls: ['./products-page.component.scss'], 
 }) 
 export class ProductsPageComponent implements OnInit { 
  // Déclaration de la liste des films 14
  datas: nomModelData[] = [];
  
  // injection du service en tant que dépendance
  consturctor(private nomService: NomService) {}
  
// Ajout de la souscription à l'observable dans ngOnInit()
ngOnInit(): void {
// On appelle la variable contenant le service,
// On indique quelle méthode on souhaite utiliser...
//On indique qu'on souhaite souscrire à l'observable
// Dans la fonction callback, on récupére les données dans une variable et on les affect à la variable datas
 this.nomService.get().subscribe((res) => {this.datas = res})
}
}
```

## Aller un peu plus loin

- Admettons que nous ayons un soucis avec notre API ou une data
- Que se passerait-il si nous avion une erreur?

### next, error, complete

Angular met à notre disposition des fonctions dans le callback de notre observable

- `next` : permet de récupérer les données
- `error` : permet de récupérer les erreurs
- `complete`: permet de récupérer le signal de fin de série et d’effectuer une action

```tsx
// on déclare notre souscription comme d'habitude
this.nomService.get.subscribe(
{
	next: data => {
		// chose à faire avec les data
	},
	
	error : error => {
	// chose à faire avec le message d'erreur
	},
	
	complete: () => {
	//chose à faire quand c'est fini
	}
})
```

### Alternatives : Les Promesses

- Les promesses sont un autre moyen de gérer les data
- Elles se basent d’avantage sur une démarche asynchrone
- Leur mise en place est un peu plus complexe

### Un cours à part entière

- Les promesse, observables, souscriptions..
- Ils sont implémentés grâce à **RxJS,**  qui pourrait faire l’objet d’une formation à part entière.
- C’est pour cette raison qu’ils ne seront pas abordés dans ce cours en detail