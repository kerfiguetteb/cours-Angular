# Routing

- Le routing nous permet de naviguer entre les différentes pages de notre navigation
- Nous n’aurons pas besoin de rafraîchissement de pages
- En réalité, ce seront les composant qui seront affiché ou non

<aside>
💡 Une page est un élément navigable, constitué de composants

</aside>

## Les routes

- Les routes sont des URLs
- Elles sont définies dans `app.routes.ts`
- Nous déclarons la route dans un tableau routes de type Routes avec pour attribut:
- `path` : l’URI de la route
- `component`: le composant à afficher

Exemple

```tsx
import { HomePageComponent } from './pages/home-page/home-page.component';
export const routes: Routes = [

    // On indique que l'URI '/home' correspond au composant HomePageComponent
    {path:'home', component:HomePageComponent},
  
];

```

- Dans `app.config.ts` nous chargeons le provider du routeur

```tsx
import { ApplicationConfig } from '@angular/core';
import { provideRouter } from '@angular/router';
import { routes } from './app.routes';

export const appConfig: ApplicationConfig = {
    providers: [
        provideRouter(routes)
    ]
};
```

> `provideRouter` prend en paramètre le tableau des routes définies précédemment. Il permet de charger le routeur dans l'application.
> 

**Utiliser les directives pour naviguer** 

- Coté html, on  remplacera les balises `href=” ”` par des balises `routerLink = “ ”`

```tsx
<a class="nav-link " routerLink="home">Home</a>
```

- Coté ts importer la directive

```tsx
  imports:[RouterLink]
```

Exemple

Je dispose de 3 pages:

- HomePage
- ProductsPage
- NotFound

Dans `app.routes.ts`

```tsx
export const routes: Routes = [
    // On indique que tous les chemins 'vides' seront renvoyés vers la page d'acceuil
    {path:'',  redirectTo : 'home', pathMatch:'full'},
    // On indique que l'URI '/home' correspond au composant HomePageComponent
    {path:'home', component:HomePageComponent},
    // idem pour l'URI '/products
    {path:'products', component:ProductsPageComponent},

    // On peut ajouter la route qui redirigera vers la page de detail du produit
    // On précise ':id' pour que l'URI contienne l'id du produit
    // {path:'product/:id', component:ProductsPageComponent},

    // Puis, que TOUTES LES AUTRES URIs qui ne sont pas trouvées
    // on va les rediriger vers le composants NotFoundComponent
    // IL DOIT TOUJOURS SE TROUVER EN BAS DE LA LISTE
    {path:'**', component:NotFoundComponent}
];

```

## Navigation dynamique et paramètre de route

- Angular permet également de passer des paramètres dans les routes et de naviguer dynamiquement.

```tsx
const routes: Routes = [
  { path: 'profile/:id', component: ProfileComponent }
];
```

- `:id` est un paramètre de route qui peut être récupéré dans le composant.
- Nous pouvons récupérer l'id grâce à ActivatedRoute.
- **`ActivatedRoute`** : Un service d'Angular qui contient des informations sur la route active, notamment les paramètres de l'URL.
- Il permet d'accéder aux données spécifiques d'une route, comme les paramètres dynamiques.

```tsx
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute } from '@angular/router';

@Component({
 //
})
export class ProfileComponent implements OnInit {
  
  // Déclaration de la propriété userId pour stocker l'identifiant utilisateur extrait de l'URL.
  // Le type string | null signifie que cette propriété peut être une chaîne ou null.
  userId: string | null = '';

  // Le constructeur de la classe injecte le service ActivatedRoute.
  // Ce service permet d'accéder aux informations sur la route active, comme les paramètres de l'URL.
  constructor(private route: ActivatedRoute) {}

  // La méthode ngOnInit est appelée automatiquement par Angular après la création du composant.
  // C'est ici que nous initialisons les données du composant.
  ngOnInit(): void {
    
    // Récupération de l'ID utilisateur à partir de l'URL.
    // snapshot capture l'état actuel de la route et paramMap est une Map qui contient les paramètres de l'URL.
    // La méthode get('id') récupère la valeur du paramètre 'id' de l'URL.
    this.userId = this.route.snapshot.paramMap.get('id');
  }
}
```

- **`OnInit`** : Une interface qui permet de définir le hook `ngOnInit`, une méthode appelée par Angular juste après la création du composant. C'est l'endroit idéal pour initialiser les données du composant.

[Cycles de vies](https://www.notion.so/Cycles-de-vies-ed373f50c24441c7bc121c2efbbf71ab?pvs=21)