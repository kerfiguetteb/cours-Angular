# Exercice

Vous devez créer une application simple qui permet de gérer une liste de tâches (to-do list) où l'utilisateur peut ajouter.

## Étapes

1. Créer un Nouveau Projet Angular
2. Créer le Composant `TodoList`
3. Mettre en Place le Modèle de Données
4. Afficher la Liste des Tâches
5. Ajouter une Nouvelle Tâche
6. Marquer une Tâche comme Terminée
7.  Supprimer une Tâche

```tsx
taches: any[] = [
    { nom: 'Acheter du lait', terminee: false },
    { nom: 'Finir le projet Angular', terminee: false },
    { nom: 'Lire un livre', terminee: true }
  ];
```