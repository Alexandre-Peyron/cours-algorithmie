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

### Class Player

Créons à présent une class pour afficher nos 2 joueurs.

Deux possibilités :
- ajouter 2 éléments dans le HTML et les lier dans notre class
- ajouter dynamiquement les élements dans le DOM depuis la class.

On va choisir la première option dans cet exemple.

Dans le HTML : 

```html
<section id="game">
    <div id="playerOne" class="player"></div>
    <div id="playerTwo" class="player"></div>
</section>
```

```css
.player {
    position: absolute;
    width: 50px;
    height: 50px;
}

#playerOne {
    background-color: brown;
}

#playerTwo {
    background-color: lightseagreen;
}

```

Côté JS, créez un nouveau fichier player.js :

```javascript
class Player {

    /**
     * @constructor
     *
     * @param app
     * @param id
     */
    constructor(app, id) {
        this.app = app;
        this.id = id;

        this.el = null; // Parent DOM Element

        // Configuration
        this.x = 0;
        this.y = 0;
        this.rotation = 0;
        this.speed = 0.2;

        this.initDOMElements();
        this.initEvents();
    }

    /**
     * Link to DOM elements
     */
    initDOMElements() {
        this.el = document.querySelector(this.id);
    }
    
    /**
    * Init listeners
    */
    initEvents() {
        
    }

    /**
     * Render view
     */
    render() {
        if (this.el == null) {
            return;
        }

        this.el.style.left = this.x + 'px';
        this.el.style.top = this.y + 'px';
    }
}
```

Dans votre class `App` vous pouvez à présent déclarer vos 2 nouveaux joueurs :

```javascript
// app.js
    /**
     * @constructor
     */
    constructor() {
        // [...]

        this.createPlayer();

        // [...]
    }
    
    createPlayer() {
        this.playerOne = new Player(this, '#playerOne');
        this.playerTwo = new Player(this, '#playerTwo');
    }
    
    render() {
        this.playerOne.render();
        this.playerTwo.render();
    }
```

Vous devez avoir 2 carrés de couleur présent sur votre page.

Dans le create player, vous pouvez jouer avec les propriétés x, y des joueurs pour changer leurs positions.

Ajoutez l'habillage que vous voulez pour rendre tout ça plus fun.

### Class Keyboard Listener

Bon, on a deux carrés colorés. ok.

On va rendre ça un peu plus interactif, en créant une classe dédié à l'écoute du clavier.

```javascript
class Keyboard {

    /**
     * @constructor
     *
     * @param topKey
     * @param leftKey
     * @param bottomKey
     * @param rightKey
     */
    constructor(topKey, leftKey, bottomKey, rightKey) {
        this.topKey = topKey;
        this.leftKey = leftKey;
        this.bottomKey = bottomKey;
        this.rightKey = rightKey;

        this.touchUp = false;
        this.touchDown = false;
        this.touchLeft = false;
        this.touchRight = false;

        this.initKeyboardListener();
    }

    /**
     * Init keyboard listener
     * `bind(this)` to keep context in callback function
     */
    initKeyboardListener() {
        document.addEventListener('keydown', this.onKeyDown.bind(this));
        document.addEventListener('keyup', this.onKeyUp.bind(this));
    }

    /**
     * On key down
     */
    onKeyDown(event) {

        // console.log('event.key', event.key);

        switch (event.key) {
            case this.topKey:
                this.touchUp = true;
                break;
            case this.leftKey:
                this.touchLeft = true;
                break;
            case this.bottomKey:
                this.touchDown = true;
                break;
            case this.rightKey:
                this.touchRight = true;
                break;
        }
    }

    /**
     * On key up
     */
    onKeyUp() {
        switch (event.key) {
            case this.topKey:
                this.touchUp = false;
                break;
            case this.leftKey:
                this.touchLeft = false;
                break;
            case this.bottomKey:
                this.touchDown = false;
                break;
            case this.rightKey:
                this.touchRight  = false;
                break;
        }
    }
}

```

Ajoutons cette class, ainsi que ça configuration dans le constructeur de notre player

```javascript
this.playerOne = new Player(this, '#playerOne', new Keyboard('z', 'q', 's', 'd'));
this.playerTwo = new Player(this, '#playerTwo', new Keyboard('ArrowUp', 'ArrowLeft', 'ArrowDown', 'ArrowRight'));
```

A présent, mettez à jour la fonction render du player, pour prendre en compte les déplacements.


### Class Bullet


### Sources

##### Assets Graphic
- [https://kenney.nl/assets](https://kenney.nl/assets)
- [https://www.gameart2d.com/freebies.html](https://www.gameart2d.com/freebies.html)
- [https://opengameart.org/](https://opengameart.org/)
- [http://untamed.wild-refuge.net/rpgxp.php](http://untamed.wild-refuge.net/rpgxp.php)
- [https://opengamegraphics.com/](https://opengamegraphics.com/)


