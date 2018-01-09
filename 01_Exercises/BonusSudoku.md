# Sudoku

> ### Définition
> Un sudoku est un groupement de tableau de 9x9 dont chaque ligne, colonne et groupe de 3x3
> contient les chiffres de 1 à 9.

Créez un script qui résout et complète le sudoku suivant :

Le but étant de compléter les tableaux ci-dessous avant de passer la variable à la fonction `generateSudoku`

```html
<div id="container">
    <table id="sudoku"></table>
</div>
```

```javascript
    var sudokuData = [
        [7, 2, '', '', 5, '', '', '', ''], ['', '', '', '', '', 9, '', 3, 8], ['', '', '', '', '', '', '', '', ''],
        ['', '', '', '', '', 3, '', '', 2], [4, '', '', '', '', '', '', '', 3], [5, '', '', 8, '', '', '', '', ''],
        ['', '', '', '', '', '', '', '', ''], [2, 5, '', 6, '', '', '', '', ''], ['', '', '', '', 3, '', '', 1, 9]   
    ]

    /**
     * @param target String Un selecteur HTML
     * @param data Array Les données du sudoku
     */
    function generateSudoku(target, data) {
        var sudoku = document.querySelector(target),
            line = null,
            row = null;

        for (var i = 0, l = data.length; i < l; i++) {
            var subArrayData = data[i],
                subArray = document.createElement('table'),
                subLine = null,
                subRow = null;
            subRow = null;

            if(i % 3 === 0) {
                line = document.createElement('tr');
                sudoku.appendChild(line);
            }

            row = document.createElement('td');
            row.appendChild(subArray);

            line.appendChild(row);

            for (var j = 0, ll = subArrayData.length; j < ll; j++) {

                if(j % 3 === 0){
                    subLine = document.createElement('tr');
                    subArray.appendChild(subLine);
                }

                subRow = document.createElement('td');
                subRow.innerText = subArrayData[j];

                subLine.appendChild(subRow)
            }
        }
    }

    generateSudoku('#sudoku', sudokuData);

```

```css
    #sudoku table td {
        width: 20px;
        height: 20px;
        text-align: center;
        border: 1px solid cadetblue;
    }
```