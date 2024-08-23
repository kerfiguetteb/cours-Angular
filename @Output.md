# @Output

- Les `output` sont un moyen de faire remonter des informations à un composant parent
- Ils utilisent des `events binding` pour faire remonter les informations
- Le but est de créer un évènement personnalisé qui sera émis par le composant enfant
- L’événement en question retournera un objet lorsqu’il sera émis.
- Le composant parent écoutera cet événement et récupérera les informations.

## La Création d’évènement

- `Angular` nous met à disposition une classe `EventEmitter`
- Cette classe peut être importée dans un composant
- Elle vient avec un constructeur et des méthodes pour gérer le cycle de vie des événements

### **EVENTEMITTER**

- La notation `<any>` permet de spécifier le type de l'événement.
- Il peut être une classe, une interface, ou un type
- Il sera renvoyé à l'émission de l'évent

### **ÉMETTRE L'ÉVÈNEMENT**

- Dans le composants enfant : `this.nomEvenement.emit(this.nomObjet)`
- Il nous appartient de choisir à quel moment l'évènement sera émis.
- Généralement, cela se fait via une méthode déclenchée par un autre événement (comme un submit, un click, etc.)
- La variable `$event` stockera le contenu de l'évènement

### `$event`

- `$event` contient les informations de l'événement (l'objet)
- Ici, il contient l'objet envoyé par `this.nomEvenement.emit(this.nomObjet)`
- On appelle event au moment de passer les infos au composant parent
- 

```html
<app-enfant (nomEventEnfant)="methodeDuParent($event)"/>
```

---

### Exemple

- Création d'un composant parent `DataCourses`
- Création d'un composant enfant `FormCourses`
- **L'enfant** enverra les infos au parent via un `@Output()`
- **Le parent** affichera la liste des courses

### 📄`form-courses.component.ts`

```tsx
export class FormCourseComponent {

  //On déclare notre Output
  @Output()
  // Il est de type EventEmitter
  // La valeur <any> correpond au type de l'objet qui sera renvoyé
  // Pour le moment on le type en any on verra plus tard pour le typer à partir d'un modèle.
  onAddArticle: EventEmitter<any> = new EventEmitter();

  // On délcare notre formulaire
  article: FormGroup = this.formBuilder.group({
    designation: ['', Validators.required],
    prix: ['', Validators.required]
  });

  // on déclare une variable qui indique si le formulaire est validé
  submitted: boolean = false;

  constructor(private formBuilder: FormBuilder) { }

  // Création d'une méthode privée pour reset mon formulaire
  private resetForm(): void {
    this.article.reset();
    this.submitted = false;
  }

  // On déclare un méthode onSubmit() qui fonctionnera au click
  public onSubmit(): void {
    this.submitted = true;
    if (this.article.valid) {
      // Si le forulaire est valide on envoie l'objet à l'écouteur
      this.onAddArticle.emit(this.article.value);
      // puis on appel la méthode reset()
      this.resetForm();
    } else {
      console.log('Formulaire invalide');
    }
  }
  // getter pour récupérer les FormControl
  get form() {
    return this.article.controls;
  }
}

```

### 📄`form-courses.component.html`

```html
<!-- Le form ici est quasi identique aux précédents -->
<!-- On a juste en levé l'affichage qui sera à la charge du parent -->

<div>
  <form [formGroup]="article" (ngSubmit)="onSubmit()">
    <div>
      <label>Désignation : </label>
      <input type="text" formControlName="designation">
      @if(submitted && form['designation'].invalid){
        <span>
          * Désignation invalide
        </span>
      }
    </div>
    <div>
      <label>Prix : </label>
      <input type="number" formControlName="prix">
      @if(submitted && form['prix'].invalid){
        <span>
          * Prix invalide
        </span>
      }

    </div>
    <div>
      <button type="submit">Ajouter</button>
    </div>
  </form>
</div>

```

### Dans 📄`data-courses.component.ts`

```tsx
export class DataCourseComponent {

  //On déclare notre liste vide 
  courses: any[] = [];

  // On définit une méthode pour ajouter un article
  addCourse(course: any): void {
    this.courses.push(course);
  }

  //On définit un getter pour afficher le total
  get total() {
    return this.courses.reduce((total, current) => total + current.prix, 0);
  }

}

```

### Dans 📄`data-courses.component.html`

```html
<!-- Appel de notre formulaire et ajout d'un event Binding -->
<!-- Lorsque l'événement est émis, on ajoute la valeur à la fonction addCourse -->
<app-form-course (onAddArticle)="addCourse($event)"></app-form-course>
```

- On peut voir que les objets générés par le formulaire sont envoyés au parent
- Le parent les récupère grâce à l’ `@Output` de l'enfant
- Il peut ensuite les afficher