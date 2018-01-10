# Génération de menu

### Objectif

Il s'agit de générer un menu `<ul><li><a href="...">[...]` depuis un tableau de données (ici en dur mais qui pourrait 
provenir d'une BDD). 

Le menu peut posséder `n` enfants, pour cela vous devez créer une fonction récursive. 

> Une fonction récursive est une fonction qui s'appelle elle-même.


Data en JavaScript :

```javascript
var menuData = [
    { title: 'Accueil', url: 'accueil.php', order: 1 },
    { title: 'Qui Sommes Nous', url: 'qsn.php', order: 2, children: [
        { title: 'L\'équipe', url: 'team.php', order: 1, children: [
            { title: 'Pierre', url: 'pierre.php', order: 1 },
            { title: 'Paul', url: 'paul.php', order: 2 },
            { title: 'Jack', url: 'jack.php', order: 3 }
        ] },    
        { title: 'Les locaux', url: 'place.php', order: 2 },    
        { title: 'La vision', url: 'vision.php', order: 2 }    
    ] },
    { title: 'Portfolio', url: 'portfolio.php', order: 3, children: [
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

Data en PHP :

```php
<?php

$menuData = [
    [ 'title' => 'Accueil', 'url' => 'accueil.php', 'order' => 1],
    [ 'title' => 'Qui Sommes Nous', 'url' => 'qsn.php', 'order' => 2, 'children' => [
        [ 'title' => 'L\'équipe', 'url' => 'team.php', 'order' => 1, 'children' => [
            [ 'title' => 'Pierre', 'url' => 'pierre.php', 'order' => 1],
            [ 'title' => 'Paul', 'url' => 'paul.php', 'order' => 2],
            [ 'title' => 'Jack', 'url' => 'jack.php', 'order' => 3]
        ]],
        [ 'title' => 'Les locaux', 'url' => 'place.php', 'order' => 2],
        [ 'title' => 'La vision', 'url' => 'vision.php', 'order' => 3],
    ]],
    [ 'title' => 'Portfolio', 'url' => 'portfolio.php', 'order' => 3, 'children' => [
        [ 'title' => 'Projet 1', 'url' => 'projet1.php', 'order' => 1],
        [ 'title' => 'Projet 2', 'url' => 'projet2.php', 'order' => 2],
        [ 'title' => 'Projet 3', 'url' => 'projet3.php', 'order' => 3],
        [ 'title' => 'Projet 4', 'url' => 'projet4.php', 'order' => 4],
        [ 'title' => 'Projet 5', 'url' => 'projet5.php', 'order' => 5],
        [ 'title' => 'Projet 6', 'url' => 'projet6.php', 'order' => 6],
        [ 'title' => 'Projet 7', 'url' => 'projet7.php', 'order' => 7],
        [ 'title' => 'Projet 8', 'url' => 'projet8.php', 'order' => 8],
        
    ]],
    [ 'title' => 'FAQ', 'url' => 'faq.php', 'order' => 5],
    [ 'title' => 'CVG', 'url' => 'cgv.php', 'order' => 4]
];
   
```

Résultat final : 

```html
<ul>
    <li><a href="accueil.php">Accueil</a></li>
    <li>
        <a href="qsn.php">Qui Sommes nous</a>
        <ul>
            <li><a href="team.php">L'équipe</a>
                <ul>
                    <li><a href="pierre.php">Pierre</a></li>
                    <li><a href="paul.php">Paul</a></li>
                    <li><a href="jack.php">Jack</a></li>
                </ul>
            </li>
            <li><a href="place.php">Les locaux</a></li>
            <li><a href="vision.php">La vision</a></li>
        </ul>
    </li>
    <li><a href="portfolio.php">Portfolio</a>
        <ul>
            <li><a href="projet1.php">Projet 1</a></li>
            <li><a href="projet2.php">Projet 2/a></li>
            <li><a href="projet3.php">Projet 3</a></li>
            <li><a href="projet4.php">Projet 4</a></li>
            <li><a href="projet5.php">Projet 5</a></li>
            <li><a href="projet6.php">Projet 6</a></li>
            <li><a href="projet7.php">Projet 7</a></li>
            <li><a href="projet8.php">Projet 8</a></li>
        </ul>
    </li>
    <li><a href="cgv.php">CGV</a></li>
    <li><a href="faq.php">FAQ</a></li>
</ul>
```