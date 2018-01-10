# Fusion de tableau

### Objectif

Il s'agit de générer un menu `<ul><li><a href="...">[...]` depuis un tableau de données (ici en dur mais qui pourrait 
provenir d'une BDD). 

Le menu peut posséder `n` enfants, pour cela vous devez créer une fonction récursive. 

> Une fonction récursive est une fonction qui s'appelle elle-même.


```javascript
var menuData = [
    { title: 'Accueil', url: 'accueil.php', order: 1 },
    { title: 'Qui Sommes Nous', url: 'qsn.php', order: 2, childs: [
        { title: 'L\'équipe', url: 'team.php', order: 1, childs: [
            { title: 'Pierre', url: 'pierre.php', order: 1 },
            { title: 'Paul', url: 'paul.php', order: 2 },
            { title: 'Jack', url: 'jack.php', order: 3 }
        ] },    
        { title: 'Les locaux', url: 'place.php', order: 2 },    
        { title: 'La vision', url: 'vision.php', order: 2 }    
    ] },
    { title: 'Portfolio', url: 'portfolio.php', order: 3, childs: [
        { title: 'Projet 1', url: 'projet1.php', order: 1 },
        { title: 'Projet 2', url: 'projet2.php', order: 2 },
        { title: 'Projet 3', url: 'projet3.php', order: 3 },
        { title: 'Projet 4', url: 'projet4.php', order: 4 },
        { title: 'Projet 5', url: 'projet5.php', order: 5 },
        { title: 'Projet 6', url: 'projet6.php', order: 6 },
        { title: 'Projet 7', url: 'projet7.php', order: 7 },
        { title: 'Projet 8', url: 'projet8.php', order: 8 }
    ] },
    { title: 'FAQ', url: 'faq.php', order: 5 },
    { title: 'CVG', url: 'cvg.php', order: 4 }
]

```
