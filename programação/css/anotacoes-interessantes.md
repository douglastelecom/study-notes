<div align='justify'>

## ANOTAÇÕES INTERESSANTES
>Acervo Pessoal
>
>16 Fevereiro 2024

#### DIREÇÃO DOS ELEMENTOS E TAMANHO AUTOMÁTICO

Quando a div pai é display-flex, as divs filhas não possuem largura máxima automaticamente, mas possuem altura máxima automática. Isso é porque por default a direção que vem é em linha `flex-direction: row`.
```html
<div style="display: flex; border: 2px solid purple; padding: 1px; height: 30%;">
    <div style="border: 2px solid red; margin: 1px;">
    </div>
    <div style="border: 2px solid blue; margin: 1px;">
    </div>
</div>
```
Veja:
![display-flex](/assets/images/css/display-flex/1.png)

Ao contrário, se a direção for mudada para em coluna `flex-direction: column`, as divs terão largura máxima e altura mínima.

```html
<div style="display: flex; flex-direction: column; border: 2px solid purple; padding: 1px; height: 30%;">
    <div style="border: 2px solid red; margin: 1px;">
    </div>
    <div style="border: 2px solid blue; margin: 1px;">
    </div>
</div>
```
Veja:
![display-flex](/assets/images/css/display-flex/2.png)

#### MARGIN

Considere a div flex abaixo com dois elementos de largura 50%:

Veja:
![display-flex](/assets/images/css/display-flex/3.png)

Se uma margem direita de 20% for acrescentada ao elemento da esquerda (o quadrado vermelho), perceba que o tamanho dos elementos diminuirá. Isso acontece porque as divs já estão ocupando todo o espaço (cada uma com 50%) então a margem precisa comprimílos para respeitar os 20% estabelecidos. Dessa forma, na prática, as divs terão na prática apenas metade de 80%, ficando cada uma com 40% de width (na prática).

```html
<div style="display: flex; border: 2px solid purple; padding: 1px; height: 30%;">
    <div style="background-color: red; width: 50%; margin: 3px 20% 3px 3px;">
    </div>
    <div style="background-color: blue; width: 50%; margin: 3px;">
    </div>
</div>
```
Veja:
![display-flex](/assets/images/css/display-flex/4.png)

#### PADDING

O padding se comporta de forma diferente. Enquanto o margin comprime ambos os elementos quando estes excedem o tamanho disponível, o padding aumenta o tamanho do seu componente e comprime os outros.

```html
<div style="display: flex; border: 2px solid purple; padding: 1px; height: 30%;">
    <div style="background-color: red; width: 50%; margin: 3px; padding-right: 20%;">
    </div>
    <div style="background-color: blue; width: 50%; margin: 3px;">
    </div>
</div>
```
Veja:
![display-flex](/assets/images/css/display-flex/5.png)

A largura da div a esquerda (vermelha) é somada com o padding da direita de 20%, que passa a ter 70% (na prática) de largura e a div a direita (azul) passa a ter apenas 30% de largura (na prática).
</div>