<div align='justify'>

## PSEUDOCLASSES E PSEUDOELEMENTS

>[smashingmagazine.com](https://www.smashingmagazine.com/2016/05/an-ultimate-guide-to-css-pseudo-classes-and-pseudo-elements/)
>
>16 Fevereiro 2024

#### SIMBOLOGIA

Pseudoclasses e pseudoelements são diferentes. Pseudoclasse se refere à um estado, enquanto o pseudolemento se refere a algum elemento acessório do elemento principal (que poderá ser tratado como um elemento html). As pseudoclasses são representadas com `:`, por exemplo `div:hover{}`, e os pseudoelementso são representados com `::`, por exemplo `div::after{}`.

#### PSEUDOCLASSES

##### ESTADO

Uma pseudoclasse de estado entá relacionada diretamente as ações do usuário.

- **Link:** representa o estado do link antes de ser clicado

```css
a:link{
    color:orange;
}
```

- **Visited:** representa o estado do link após de ser clicado

```css
a:visited{
    color:blue;
}
```

- **Hover:** estiliza qualquer elemento quando o ponteiro está em cima:

```css
a:hover{
    color:purple;
}
```

- **Active:** funciona sempre que um elemento é "ativado", ou seja no tempo entre o click e o soltar do botão.

```css
a:active{
    color:rebeccapurple;
}
```
- **Focus:** ativa sempre que um dispositivo apontador, como teclado, touchscreen ou mouse o seleciona.
```css
a:focus{
    color:green;
}
//ou
input:focus{
    color:green;
}
```

##### ESTRUTURAL

- **First-Child:** seleciona sempre o primeiro elemento de um elemento pai.

```html
<ul>
    <li>This text will be orange.</li>
    <li>Lorem ipsum dolor sit amet.</li>
    <li>Lorem ipsum dolor sit amet.</li>
</ul>
```

```css
li:first-child {
    color: orange;
}
```

- **First of Type:** seleciona sempre o primeiro filho de cada tipo. No exemplo abaixo, tanto a primeira `<li>` quanto o primeiro `<span>` serão laranja.

```html
<ul>
    <li>This text will be orange.</li>
    <li>Lorem ipsum dolor sit amet. <span>This text will be orange.</span></li>
    <li>Lorem ipsum dolor sit amet.</li>
</ul>
```

```css
ul :first-of-type {
    color: orange;
}
```

- **Last Child:** representa o último elemento filho do seu elemento pai.

```html
<ul>
    <li>Lorem ipsum dolor sit amet.</li>
    <li>Lorem ipsum dolor sit amet.</li>
    <li>This text will be orange.</li>
</ul>
```

```css
li:last-child {
    color: orange;
}
```
- **Last of Type:** representa o último elemento de cada tipo do seu elemento pai.

```html
<ul>
    <li>Lorem ipsum dolor sit amet. <span>Lorem ipsum dolor sit amet.</span> <span>This text will be orange.</span></li>
    <li>Lorem ipsum dolor sit amet.</li>
    <li>This text will be orange.</li>
</ul>
```

```css
li:last-of-type {
    color: orange;
}
```

- **Not:** pseudoclasse de negação. Aceita um argumento entre parênteses — basicamente outro seletor — e os elementos não serão afetados pela estilização.

```html
<ul>
    <li class="first-item">Won't be orange</li>
    <li>Lorem ipsum dolor sit amet.</li>
    <li>Lorem ipsum dolor sit amet.</li>
    <li>Lorem ipsum dolor sit amet.</li>
</ul>
```

```css
li:not(.first-item) {
    color: orange;
}
```

O not também pode ser encadeado da seguinte forma:

```css
li:not(.first-item):not(:last-of-type) {
    background: yellow;
    color: black;
}
```

**Nth Child:** Seleciona um elemento filho específico.

```html
<ol>
    <li>Alpha</li>
    <li>Beta</li>
    <li>Gamma</li>
    <li>Delta</li>
    <li>Epsilon</li>
    <li>Zeta</li>
    <li>Eta</li>
    <li>Theta</li>
    <li>Iota</li>
    <li>Kappa</li>
</ol>
```

Com o css baixo apenas o `<li>` Beta será laranja:

```css
ol :nth-child(2) {
    color: orange;
}
```

Agora, com esse css abaixo os elementos que serão laranja são Beta, Delta, Zeta, Theta e Kappa. Sempre de dois em dois.

```css
ol :nth-child(2n) {
    color: orange;
}
```

Agora ele irá selecionar de dois em dois, mas só a partir do sexto. Dessa forma apenas Zeta, Theta e Kappa serão laranja.

```css
ol :nth-child(2n+6) {
    color: orange;
}
```

Agora todos os elementos pares serão laranja:

```css
ol :nth-child(even) {
    color: orange;
}
```

**Nth Last Child:** O mesmo que foi feito com nth-child pode ser feito com nth-last-child, mas com a contagem inversa (do último ao primeiro).

```css
ol :nth-last-child(2n) {
    color: orange;
}
```

**Nth of Type:** Seleciona o enésimo elemento de um determinado tipo.

```css
p:nth-of-type(2) {
    color: orange;
}
```

**Nth last of type** Seleciona o enésimo elemento de um determinado tipo, porém com a contagem inversa (do último para o primeiro).

```css
p:nth-last-of-type(2) {
    color: orange;
}
```

**Only Child:** tem como alvo o único filho de um elemento pai. Se o elemento pai tiver mais de um filho, nenhum será afetado. Repare abaixo que apenas o `<li>` do primeiro `<ul>` será afetado, pois só ele possui um único filho.

```html
<ul>
    <li>This text will be orange.</li>
</ul>

<ul>
    <li>Lorem ipsum dolor sit amet.</li>
    <li>Lorem ipsum dolor sit amet.</li>
</ul>
```

```css
ul :only-child {
    color: orange;
}
```

**Only of type:** semelhante ao `only-child`, porém apenas funciona se o elemento não tiver um irmão do mesmo tipo.

</div>