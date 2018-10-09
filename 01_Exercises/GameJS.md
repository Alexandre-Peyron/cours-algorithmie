# Game POO JS

### Objectif
Le but ici est de créer un jeu multijoueurs en javaScript orienté objet.

Le jeu doit mettre en scène plusieurs éléments centraux (voitures, vaisseaux, autres...)
gérés au clavier par les utilisateurs.

Il peut s'agir d'un affrontement, d'une course...

La thématique est libre.

Les points importants à abordés sont :
- évènements clavier
- générations d'éléments aléatoires
- déplacements
- gestion des collisions
- POO

Pas de framework, pas de webpack, pas de gulp, simplement du HTML/CSS/JS.


#### Structure de base

Ci-dessous, la structure de base du projet sur laquelle vous pouvez commencer :


```html
<!--index.html-->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Game</title>
    <link rel="stylesheet" type="text/css" href="app/css/app.css" >
</head>
<body onload="init()">
    <div id="app">
        <section id="game">
            <!-- Eléments de votre jeu -->
        </section>
        <section id="ui">
            <!-- Interface utilisateur -->
        </section>
    </div>

    <!-- Fichiers JS à ajouter ici -->
    <script type="text/javascript" src="app/js/app.js"></script>
    <script type="text/javascript">
        function init(){
            const app = new App();
        }
    </script>
</body>
</html>
```

Le fichier css de base :
```css
/*app.css*/
body, html {
    height: 100%;
    width: 100%;
}

* {
    margin: 0;
    padding: 0;
}

/* APP */

#app {
    height: 100%;
    width: 100%;
    overflow: hidden;
}


#game, #ui {
    position: relative;
    width: 100%;
    height: 100%;
}

```

Body, HTML, app, game et ui sont en full screen.


```javascript
// app.js
class App {

    /**
     * @constructor
     */
    constructor() {
        this.initDOMElements();
        this.initEvents();

        this.loop();
    }

    /**
     * Link to DOM elements
     */
    initDOMElements() {
        this.el = document.querySelector('#app');
    }

    /**
     * Events
     */
    initEvents() {

    }

    /**
     * Eternal loop
     */
    loop() {
        var self = this;

        // Méthode JS qui s'exécute à chaque rafraichissement d'image du navigateur 
        requestAnimationFrame(function () {
            self.render();
            self.loop();
        })
    }

    /**
     * Render App and all views
     */
    render() {
        
    }
}
```

La classe App est le point d'entrée de notre application.

On va essayer de structurer toute nos class ainsi pour plus de lisibilité :

- un constructeur
- initDOMElements : qui fait le lien avec les éléments déjà présents dans le DOM si nécessaire
- initEvents : mise en place des listeners
- render : qui rafraichit l'affichage de nos éléments à chaque itération de loop

La méthode loop, est un pattern de conception très souvent utilisé dans les jeux vidéo.
Il s'agit d'une boucle, qui se répète de manière infini à une cadence de 24 à 60 images par seconde en fonction de la puissance de calcul.
Les éléments du jeu, les déplacements, les collisions sont rendus/calculés à chaque itération.

### Class Keyboard Listener



### Class Player 


### Class Bullet


### Sources

##### Assets Graphic
- [https://kenney.nl/assets](https://kenney.nl/assets)
- [https://www.gameart2d.com/freebies.html](https://www.gameart2d.com/freebies.html)
- [https://opengameart.org/](https://opengameart.org/)
- [http://untamed.wild-refuge.net/rpgxp.php](http://untamed.wild-refuge.net/rpgxp.php)
- [https://opengamegraphics.com/](https://opengamegraphics.com/)


