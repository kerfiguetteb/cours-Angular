# Inputs

> La communication Parent → Enfant dans Angular se fait principalement à travers les Inputs. Voici les points clés :
> 
- Les Inputs sont des informations passées au composant enfant lors de son appel
- Ils sont similaires aux 'props' en React
- Ils permettent au composant enfant de récupérer et utiliser ces informations
- Cette approche rend les composants génériques, dynamiques et versatiles

L'utilisation des Inputs permet donc de transmettre des données du composant parent vers le composant enfant, rendant ainsi la communication et le partage d'informations plus flexibles et réutilisables.

## **CONTEXTE**

- Rappel : un composant doit être générique
- Ça implique d'être capable de le rendre dynamique et versatile

### **EXEMPLE**

- Je veux créer un bouton générique, avec son style
- Le bouton ne fera pas forcément toujours la même chose

> Parfois un message, parfois un autre
> 
- Le titre du bouton doit donc être capable de changer en fonction des besoins

### **Bouton d'alertes génériques**

- Création d'un composant `GenericAlertButton`

```tsx
ng g c genericAlertButton
```

- Il affichera un message d'alerte lorsque cliqué

> NB : On va utiliser des alertes MAIS c'est pas bien ! En effet, ça coupe le flux de l'application
> 

### Dans 📄 generic-alert-button.component.ts

```tsx
export class GenericAlertButtonComponent {

  // Propriété d'entrée `buttonTitle` définie avec le décorateur `@Input`
  @Input()
  buttonTitle!: string;

  // Propriété d'entrée `alertMessage` définie avec le décorateur `@Input`
  @Input()
  alertMessage!: string;

  // Méthode `afficheAlert` appelée lorsqu'un événement de clic se produit sur le bouton
  afficheAlert() {
    // Affiche une boîte de dialogue avec le message d'alerte spécifié
    alert(this.alertMessage);
  }

```

### Dans 📄generic-alert-button.component.html

```html
<!-- Bouton avec gestionnaire d'événement `click` -->
<!-- Lorsque ce bouton est cliqué, il appelle la méthode `afficheAlert()` du composant correspondant -->
<button (click)="afficheAlert()">{{buttonTitle}}</button>

```

### Dans 📄app.component.html

```html
<app-generic-alert-button buttonTitleEnfant="Ping" alertMessageEnfant="Pong"></app-generic-alert-button>
<app-generic-alert-button buttonTitleEnfant="Marco" alertMessageEnfant="Polo"></app-generic-alert-button>
<app-generic-alert-button buttonTitleEnfant="Philippe !" alertMessageEnfant="Je sais où tu te caches !!"></app-generic-alert-button> -->

```

- Nous avons vu qu'en appelant plusieurs fois un bouton avec des input différents, nous obtenons un message d'alerte différent
- Le souci est que les data sont données en brut dans la balise

## **@INPUT ET PROPERTY BINDING**

### **PROPERTY BINDING**

- Il est également possible de récupérer les informations depuis un composant parent
- Ce qui permet d'éviter d'avoir à coder les données en 'dur' dans la balise.
- Pour ce faire, on utilisera les crochets `[xx]` pour récupérer les données

### Exemple

- Nous allons créer un parent `ButtonMenu`

```html
ng g c buttonMenu
```

- Il appellera notre ancien composant `GenericAlertButton`
- C'est lui qui lui passera les data via le **property binding**

### Dans 📄button-menu-component.ts

```tsx
export class ButtonMenuComponent {

  // Déclaration de la propriété `buttons`, qui est un tableau d'objets.
  buttons: any[] = [
    {
      // Chaque objet du tableau représente un bouton avec un titre et un message d'alerte.
      buttonTitle: "Philippe",
      alertMessage: "Je sais où tu te caches!!!!!!"
    },
    // Vous pouvez ajouter autant d'objets que nécessaire pour définir différents boutons et messages.
    {
		    ...
	  }
  ]

```

### Dans 📄button-menu-component.html

```html
<!-- Ici nous sommes dans notre composant Parent -->

<!-- Boucle `@for` pour itérer sur chaque élément de la collection `buttons`.
     `item` représente l'élément courant et `track $index` est utilisé pour suivre l'index de chaque élément. -->
     @for (item of buttons; track $index) {
        <!-- Création d'une instance du composant `app-generic-alert-button` pour chaque élément de la collection `buttons`.
             Les propriétés `alertMessage` et `buttonTitle` de chaque élément `item` sont passées aux entrées correspondantes du composant. -->
        <app-generic-alert-button [alertMessage]="item.alertMessage" [buttonTitle]="item.buttonTitle"></app-generic-alert-button>
    }@empty {
	    <!-- message si vide -->
    }

```

- Nous avons pu afficher dynamiquement notre composant
- A terme, nous verrons comment faire la même chose depuis une API