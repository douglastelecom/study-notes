<div align='justify'>

## ANOTAÇÕES INTERESSANTES

>[Link](https://angular.io/guide/animations)
>
>16 Fevereiro 2024

#### TAMANHO DAS DIVS

Uma div, quando não possui suas dimensões definidas (width and height), sempre começa com largura máxima disponível e altura mínima.

```html
<div style="border: 2px solid red;">
</div>
```

<div style="border: 2px solid red;">
</div>

Se a div pai não tem um tamanho estabelecido, ela sempre se adequa ao tamanho dos seus elementos filhos.



```html
<div style="border: 2px solid red;">
    <div style="border: 2px solid blue; height: 20%;">
    </div>
</div>
```
 Veja:
<div style="border: 2px solid red;">
    <div style="border: 2px solid blue; height: 20%;">
    </div>
</div>

Quando a div pai possui um tamanho estabelecido, ela não se adequa as divs filhas, mas as divs filhas que se adequam a ele. Além disso, também perceba que a largura da div filha sempre se adequa ao tamanho máximo disponível. O mesmo não acontece com a altura.

```html
<div style="border: 2px solid red; height: 20%">
    <div style="border: 2px solid blue; height: 20%;">
    </div>
</div>
```
 Veja:
<div style="border: 2px solid red; height: 20%">
    <div style="border: 2px solid blue; height: 20%;">
    </div>
</div>

#### DISPLAY FLEX

Quando a div pai é display-flex, as divs filhas não possuem largura máxima automaticamente.
```html
<div style="display: flex; border: 2px solid purple; padding: 1px;">
    <div style="border: 2px solid red; margin: 1px;">
    </div>
    <div style="border: 2px solid blue; margin: 1px;">
    </div>
</div>
```
Veja:
<div style="display: flex; border: 2px solid purple; padding: 1px;">
    <div style="border: 2px solid red; margin: 1px;">
    </div>
    <div style="border: 2px solid blue; margin: 1px;">
    </div>
</div>





</div>