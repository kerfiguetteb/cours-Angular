# Bindings

## **ONE WAY BINDING** {{xx}}

- Le Binding permet de faire passer des données du composant vers sa vue (page HTML)
- On utilisera la 'double moustache'  {{xx}} directement dans la vue

### **Explication**

- 📄xx.component.ts étant une classe, on peut y stocker de l'information via des attributs
- Cette information peut être récupérée via le binding pour être affichée
- Procéder ainsi contribue à rendre nos composants dynamiques

### **Exemple** 🧐**:**

- Création du component User :

```powershell
 ng g c User
```

- Dans 📄user.component.ts , ajout d'attributs nom et prénom à notre classe

```tsx
import { Component } from '@angular/core';

@Component({
  selector: 'app-user',
  standalone: true,
  imports: [FormsModule],
  templateUrl: './user.component.html',
  styleUrl: './user.component.css'
})
export class UserComponent {

  nom :string = "John";
  prenom :string = "Doe";

}

```

- Appel des attributs dans 📄user.component.html, en utilisant 'double moustache'.

```html
<!-- Titre de composant -->
<h2>Utilisateur</h2>

    <p>{{ nom }}</p>      <!-- Affiche le nom -->
    <p>{{ prenom }}</p>   <!-- Affiche le prénom -->

```

- Importation du composant UserComponent dans📄app.component.ts

```tsx
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [
    RouterOutlet,
    UserComponent,
    
    ],
  templateUrl: './app.component.html',
  styleUrl: './app.component.css'
})
export class AppComponent {
  title ?:string;
}

```

- Appel du composant UserCompent avec la balise HTML dans📄app.component.html

```html
<app-user></app-user>
<router-outlet/>

```

Une fois fait, on peut retrouver l'affichage suivant:

```html
Utilisateur

Nom : John

Prenom : Doe
```

### **En résumé** 🤔

- La double moustache permet donc d'injecter des datas dans la vue
- On appelle ça l'interpolation
- Si les données du modèle (Classe) sont modifiées, alors l'affichage sera modifié

## **PROPERTY BINDING** [xx]

- Le property binding permet de valoriser une propriété d'un composant depuis le modèle
- ll permet entre autres de remplir les attributs d'une balise HTML dynamiquement
- On crée un lien entre cet attribut et une propriété du composant
- On utilise la notation suivante : [xx]

### **Exemple** 🧐**:**

- Supposons que l'on souhaite ajouter une image à mon dernier composant.
- On peut lui ajouter un attribut imgUrl qui contiendra l'url de l'image
- Nous pourrions faire appel à cet attribut en tant qu'attribut de la balise <img>

### Dans 📄user.component.ts

```tsx
import { Component } from '@angular/core';

@Component({
  selector: 'app-user',
  standalone: true,
  imports: [FormsModule],
  templateUrl: './user.component.html',
  styleUrl: './user.component.css'
})
export class UserComponent {

  nom :string = "John";
  prenom :string = "Doe";
  imgUrl :string = "https://picsum.photos/200/300"

}

```

### Dans 📄user.component.html

```html
<!-- Image de profil -->
<!-- J'utilise le property binding pour envoyer l'image dans ma balise
 src : attribut html à modifier
 imageUrl : nom de l'attribut de ma classe
  -->
 
<img [src]="imgUrl" alt="">
```

### **En résumé**

- En utilisant le property binding, j'ai pu afficher l'image dans ma vue
- Nous n'avons pas eu à coder l'image directement dans la balise
- Nous sommes allés chercher l'attribut contenant les informations dans la classe.

## **TWO WAY BINDING** [(xx)]

- Two way binding d'envoyer des informations à notre modèle depuis la vue
- Utile pour les input/formulaires par exemple
- On utilise alors la notation suivante : [(xxx)]

### **Exemple** 🧐**:**

- Pour cet exemple, il faut d'abord ajouter un module.

### 📄user.component.ts

```tsx
import { Component } from '@angular/core';

@Component({
  selector: 'app-user',
  standalone: true,
  imports: [FormsModule],
  templateUrl: './user.component.html',
  styleUrl: './user.component.css'
})
export class UserComponent {

  nom :string = "John";
  prenom :string = "Doe";
  imgUrl :string = "https://picsum.photos/200/300"
  job:string = "";

}

```

### 📄user.component.html

```html
<form action="">
     <!-- Liaison bidirectionnelle avec la variable `job` -->
    <input type="text" name="jobLabel" [(ngModel)]="job"> 
</form>

<!-- Affichage du métier -->
<p>{{ job }}</p>  <!-- Affiche le métier actuel -->

```

- Sur la page de votre application, ajoutez des informations dans l' input.
- Les informations apparaissent en 'live' sur la page

## **LES EVENT BINDING** (xx)

- Il est possible réagir à des évents JS déclenchés depuis la vue.
- Ce type d'événement est appelé event binding
- Il déclenche une action dans notre composant.
- On ajoutera une méthode dans la classe de notre composant
- Coté html, on ajoutera un attribut comme suit : (event) = 'méthode'

**LES TYPES D'EVENTS**

```markdown
(clcik)="myFunction"
(dbclcik)="myFunction"
(submit)="myFunction"
(blur)="myFunction"
(focus)="myFunction"
(scroll)="myFunction"
(cut)="myFunction"
(copy)="myFunction"
(paste)="myFunction"
(keyup)="myFunction"
(keypress)="myFunction"
(mouseup)="myFunction"
(mousedown)="myFunction"
(mouseenter)="myFunction"
```

### **Exemple** 🧐**:**

- Création d'un composant : AlertButton

```tsx
ng g c alertButton
```

- Son but est de présenter un bouton qui affichera une alerte lors du clic

### 📄alert-button.component.ts

```tsx
import { Component } from '@angular/core';

@Component({
  selector: 'app-alert-button',
  standalone: true,
  imports: [],
  templateUrl: './alert-button.component.html',
  styleUrl: './alert-button.component.css'
})
export class AlertButtonComponent {
  
  //ajoute une méthode onCLick() dans ma classe
  onClick(){
    alert('tu as tout cassééééééé')
  }

} 
```

### Ajout du bouton dans la vue :📄alert-button.component.html

```html
<h2>AlertButton event</h2>
<!-- Création du bouton avec ecouteur d'evenement click -->
<button (click)="onClick()" >Clic</button>
```

### Appel du composant dans 📄app.component.html

```html
<app-alert-button></app-alert-button>
```

### Appel du composant dans 📄app.component.ts

```tsx
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [
    RouterOutlet,
    UserComponent,
    // import du composant AlertButton
    AlertButtonComponent
    
    ],
  templateUrl: './app.component.html',
  styleUrl: './app.component.css'
})
export class AppComponent {
  title ?:string;
}
```

[Exercice](Exercice%20231218001c1141da94c90ac78e691a86.md)