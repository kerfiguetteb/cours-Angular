# contrôle de flux

## **L'INSTRUCTION @FOR**

- La directive @for permet de parcourir une liste.
- Il s'agit d'une instruction forEach qui permet d'itérer sur chaque élément de la liste contenue dans le contrôleur

### **CRÉATION D'UN COMPOSANT :** Liste

```tsx
ng g c liste
```

- Son but est de présenter une liste de noms
- On y ajoute à notre contrôleur un attribut items qui contiendra une liste de noms

### 📄list.component.ts

```tsx
import { Component } from '@angular/core';

@Component({
  selector: 'app-liste',
  standalone: true,
  imports: [],
  templateUrl: './liste.component.html',
  styleUrl: './liste.component.css'
})
export class ListeComponent {

  // On déclare ici notre liste de prénoms
  items: string[] = ['Carlos', 'foo', 'bar'];

}
```

### Ajout de la directive dans la vue :📄liste.component.html

```html
<!--On itère sur items(tableaux) et on crée une variable element à chaque itération -->
<!--items corresponds au nom de notre variable contenant la liste -->
<!-- element correspond au nom de la variable contenant la valeur de chaque itération -->
@for (element of items; track $index) {
    <p>{{element}} - {{$index}}</p>
}@empty {
    <p>Aucun utilsateur</p>
}
```

- @empty : alternative si la collection est vide
- element: représente l'élément courant de items lors de l'itération.
- items: la collection ( tableau ) sur laquelle itérer.
- track: indique à Angular comment suivre les éléments de la collection. Cela permet à Angular de mettre à jour correctement les éléments de la liste lorsqu'ils changent.

Toutes les variables particulières commencent par $ et sont réservées pour les blocs @for. Voici d'autres exemples de variables spéciales :

- $index : l'index de l'élément courant dans la collection.●$first : true si l'élément courant est le premier de la collection.
- $last : true si l'élément courant est le dernier de la collection.
- $even : true si l'index de l'élément courant est pair.
- $odd : true si l'index de l'élément courant est impair.
- $count : le nombre total d'éléments dans la collection.

### **AFFICHAGE CONDITIONNEL**

- Il existe plusieurs manières d'afficher ou de masquer un élément :
- L'attribut [hidden]
- La directive @if

### **HIDDEN**

- Avec l'attribut [hidden], on cachera l'élément si la condition est vraie.
- On ajoute cet attribut en déclarant un attribut hidden dans la balise HTML à afficher/cacher

### **LA CONDITION**

- La condition en question sera vérifiée et retournera un booléen.
- Le fonctionnement sera similaire à la vérification d'une condition dans un if

## **Création d'un composant 'Magie'**

```html
ng g c magie
```

- On y ajoutera un attribut de type boolean
- On ajoutera une méthode pour modifier cet attribut
- On intégrera cette méthode dans un bouton grâce à l'event binding

### 📄magie.component.ts

```tsx
export class MagieComponent {
  // Déclaration d'un booléen avec une valeur par défaut sur true
  hidden: boolean = false;

  // Méthode pour modifier le booléen en inversant sa valeur
  toogle(){
    this.hidden = !this.hidden
  }
}

```

### 📄magie.component.html

```html
<!-- On ajoute un bouton pour afficher / cacher le contenu de la balise
on utiise l'event binding pour appeler la méthode toggle lors du clic sur le bouton -->
<button (click)="toogle()">abracadabra!!!!!</button>

<!-- Contenue de la balise afficher /cacher
Ici se sera juste un texte mais on peut y mettre ce qu'on veut ex : un composant :) -->
<p [hidden]="hidden">c'est comme par magie</p>

```

- Avec [hidden], la balise est tout de même générée dans le code.
- On peut vérifier sa présence dans la console.

### **@If**

- La directive @if permet d'afficher un élément si la condition est vraie.
- Contrairement à l'attribut [hidden], la directive @if ne génère pas la balise dans le code.

```html
<button (click)="toogle()">abracadabra!!!!!</button>

@if (hidden) {
    <p>c'est comme par magie</p>
}

```

### **Liste filtrée**

- Création d'un composant 'ListeFiltre'

```html
ng g c listFiltre
```

- On créera une liste d'utilisateurs
- On y affichera uniquement les utilisateurs qui ont un nom comportant la lettre 'a'

### Ajout de la liste dans 📄liste-filtre.component.ts

```tsx
export class ListeComponent {
  // On déclare ici notre liste de prénoms
   items: string[] = ['Carlos', 'foo', 'bar', 'Jimi', 'Stevie Nicks'];

}

```

### Ajout de la condition dans 📄liste-filtre.component.html

```html
<!-- Création d'une balise qui affichera un paragraphe pour chaque item -->
<h2>liste-filtre works!</h2>

@for (item of items; track $index) {
  <!-- Item qui ne sera affiché que si il contient un 'a' -->
  <!--  On fait appel à la méthode 'includes()' de JS directement dans le *ngIf -->
    @if (item.includes('a')) {
        <p>{{item}}</p>
    }
}

```

## **Les pipes**

- Une pipe | permet de transformer la donnée au moment de l'affichage.
- On pourra entre autres filtrer la donnée ou la traiter
- On pourra par exemple changer l'affichage d'une date pour coller au format français.
- Une pipe peut être appelée directement lorsqu'on utilise une double moustache {{ }}
- Par exemple, pour afficher la date du jour, on utilisera la pipe date :

### Nous avons un composant 📄show-date.component.ts qui affiche la date du jour.

Il possède le module CommonModule

```tsx
impotrs: [DatePipe]
```

Il possède une variable today qui contient la date du jour.

```tsx
today :Date = new Date();
```

Nous souhaitons afficher la date du jour dans un paragraphe.

```html
<p>Nous sommes le {{ today | date }}</p>
```

Nous obtenons le retour avec le format suivant : Mois Jour, Année

Angular nous permet de passer des arguments aux pipes. On utilise alors le :

Nous obtenons alors le code suivant:

```html
<p>Nous sommes le {{ today | date :"dd/MM/yy" }}</p>
```

## **LES PIPES ANGULAR**

Angular propose déjà un certain nombre de pipes:

- **uppercase / lowercase** : transforme une chaîne en majuscule ou en minuscule
- **date** : transforme une date en chaîne de caractères
- **currency** : transforme un nombre en devise
- **number** : transforme un nombre en chaîne de caractères
- **json** : transforme un objet en chaîne de caractères
- **slice / replace / trim** : qui fonctionnent comme les méthodes éponymes de javascript
- **titlecase** : permet de mettre en majuscule la première lettre d'une chaîne de caractères
- **percent** : permet de mettre en pourcentage une valeur

> PS : Pensez à importer **CommonModule** dans vos composants pour pouvoir utiliser les Pipes d’Angular
>