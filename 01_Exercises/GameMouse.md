# Follow Mouse

### Objectif
Créer un ou N élément(s) qui vont suivre les déplacements de votre curseur.

- Première chose, trouver une image à utiliser 

![http://www.icone-png.com/png/21/21475.png](http://www.icone-png.com/png/21/21475.png)

- ajouter l'image dans le dom
- créer une boucle infinie, qui à chaque itération, récupère la position du curseur et l'applique à votre image.

```javascript
document.onmousemove = function(){};
```

- faire en sorte que la pointe de l'image de la souris soit toujours orientée vers votre curseur
- ajouter un délai de 200ms avant de déplacer l'image
- ajouter N images qui fonctionnement de la même manière dont le délai sera `200ms*N`
