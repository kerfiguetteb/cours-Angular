# arborescence

## MA PREMIÈRE APP

L'architecture d'une application Angular est la suivante. Tous ou presque sont essentiels au fonctionnement de Angular

![image1.jpg](image1.jpg)

### **Le répertoire app 📁**

- C'est ici que l'on ajoutera les composants Angular
- On y créera un dossier components 📁

### **app.component.ts** 📄

- Contient le composant principal de l'application
- Il dispose de son propre style style.css

### **app.component.html** 📄

- Page HTML du composant app.component.ts
- Correspond au body de notre application
- C'est ici que l'on appellera les différents composants que l'on créera

### **app.routes.ts**📄

- Permet de définir les routes de l'application

### **index.html**📄

- Le composant principal app.component.ts est importé dans index.html
- On ajoute le composant principal dans le <body> , comme une balise HTML
- On l'ajoute sous l'appellation app-root : <app-root></app-root>

### **🌐 En Résumé :**

- index.html est le point de départ de notre application
- index.html appelle le composant principal
- app.component.ts grâce à la balise <app-root></app-root> app.component.ts est le composant principal de notre application
- De la même manière, on appellera nos composants dans app.component.html

💡 [structure des fichiers](https://angular.fr/get_started/structure.html)