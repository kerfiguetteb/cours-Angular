# les composants

**Les composants**

💡

## **Définition** 🧐

- Comme expliqué en introduction, un composant est une des nombreuses briques qui constituent notre application
- Un composant se veut générique, réutilisable et spécialisé
- Notre page sera alors constituée de plusieurs composants

## **Créer un composant**

- On peut créer un composant avec la commande:

```tsx
ng generate component nom du composant
```

ou

```tsx
ng g c nom du composant
```

- Lorsque l'on utilise la commande pour créer un composant, angular génère tous les fichiers nécessaires

## **Faites le test !**

Tapez la commande suivantes :

```tsx
ng g c components/FirstComponent
```

**Création des fichiers**

La commande crée les fichiers suivants:

```markdown
src
| |
| components
| | |firsst-component
| | | |
| | | first-component.component.html # Fichier HTML
| | | first-component.component.css # Feuille de style
| | | first-component.component.spec.ts # Fichier de test
| | | first-component.component.ts # Classe du composant
```

## **Composant = Classe !**

- Un composant est une classe en TypeScript
- Il pourra être manipulé comme tel, et bénéficier de méthodes / attributs accessibles par la vue
- Son décorateur @Component nous permet d'indiquer à Angular que c'est un composant

## **first-component.component.ts**

```tsx
import { Component } from '@angular/core';

// Décorateur qui définit les métadonnées pour le composant
@Component({
  // Indique le nom de la balise HTML de notre composant
  selector: 'app-first-component',

  // Indique que ce composnat est autonome et peut fonctionner sans être déclaré dans un module
  standalone: true,

  // Permet d'importer d'autres composants, directive, ou pipes nécessaure pour ce composnat
  imports: [],

  // Indique l'emplacement du fichier HTML associé au composant
  templateUrl: './first-component.component.html',

  // Indique l'emplacement de la feuille de style CSS associée au composant
  styleUrl: './first-component.component.css'
})

// Déclaration de la classe du composant
export class FirstComponentComponent {

  // Ajoutez ici les propriétés et les méthodes de votre composant

}

```