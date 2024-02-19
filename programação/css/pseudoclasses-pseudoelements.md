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

- **:link** representa o estado do link antes de ser clicado

```css
a:link{
    color:orange;
}
```

- **:visited** representa o estado do link após de ser clicado

```css
a:visited{
    color:blue;
}
```

- **:hover** estiliza qualquer elemento quando o ponteiro está em cima:

```css
a:hover{
    color:purple;
}
```

- **:active** funciona sempre que um elemento é "ativado", ou seja no tempo entre o click e o soltar do botão.

```css
a:active{
    color:rebeccapurple;
}
```
- **:focus** ativa sempre que um dispositivo apontador, como teclado, touchscreen ou mouse o seleciona.
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

- **:first-child** seleciona sempre o primeiro elemento de um elemento pai.

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

- **:first-of-type** seleciona sempre o primeiro filho de cada tipo. No exemplo abaixo, tanto a primeira `<li>` quanto o primeiro `<span>` serão laranja.

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

- **:last-child** representa o último elemento filho do seu elemento pai.

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
- **:last-of-type** representa o último elemento de cada tipo do seu elemento pai.

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

- **:not()** é a pseudoclasse de negação. Aceita um argumento entre parênteses — basicamente outro seletor — e os elementos não serão afetados pela estilização.

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

**:nth-child()** seleciona um elemento filho específico.

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

**:nth-last-child()** faz o mesmo que foi feito com nth-child pode ser feito com nth-last-child, mas com a contagem inversa (do último ao primeiro).

```css
ol :nth-last-child(2n) {
    color: orange;
}
```

**:nth-of-type()** seleciona o enésimo elemento de um determinado tipo.

```css
p:nth-of-type(2) {
    color: orange;
}
```

**:nth-last-of-type()** seleciona o enésimo elemento de um determinado tipo, porém com a contagem inversa (do último para o primeiro).

```css
p:nth-last-of-type(2) {
    color: orange;
}
```

**:only-child** tem como alvo o único filho de um elemento pai. Se o elemento pai tiver mais de um filho, nenhum será afetado. Repare abaixo que apenas o `<li>` do primeiro `<ul>` será afetado, pois só ele possui um único filho.

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

**:only-of-type** é semelhante ao `only-child`, porém apenas funciona se o elemento não tiver um irmão do mesmo tipo.

**:target** é ativado em um determinado elemento com id e path da url iguais. 

URL: https://awesomebook.com/#target

```html
<article id="target">
    <h1><code>:target</code> pseudo-class</h1>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit!</p>
</article>
```

```css
:target {
    background: yellow;
}
```

##### VALIDAÇÃO

Pseudoclasses que funcionam bem com formulários, mas que também podem ser usadas com outros tipos de elementos html.

**:checked**

Ativa quando um determinado checkbox ou um determinado radio button foi selecionado.

```css
:checked + label {
    background: $g;
    transition: .3s;
}
```

**:default** também bastante utilizado em radiobuttons e checkboxs. É utilizado para os valores default do radiobutton ou do checkboxe. Por exemplo, no radiobutton abaixo, o css será aplicado apenas na season de id summer, que tem o atributo "checked" (que o torna o default):

```html
<fieldset>
  <legend>Favorite season</legend>

  <input type="radio" name="season" id="spring" value="spring" />
  <label for="spring">Spring</label>

  <input type="radio" name="season" id="summer" value="summer" checked />
  <label for="summer">Summer</label>

  <input type="radio" name="season" id="fall" value="fall" />
  <label for="fall">Fall</label>

  <input type="radio" name="season" id="winter" value="winter" />
  <label for="winter">Winter</label>
</fieldset>
```

```css
input:default {
  box-shadow: 0 0 2px 1px coral;
}

input:default + label {
  color: coral;
}
```

**:disabled** tem como alvo o elemento que está desabilitado.

```html
<input type="text" id="name" disabled>
```

```css
:disabled {
    opacity: .5;
}
```

**:empty** é utilizado para elementos que estão vazios, como um input que não possui um único character digitado ou uma div que não possui nenhuma escrita.

```html
<div>This box is orange</div>
<div> </div>
<div></div>
<div><!-- This comment is not considered content --></div>
```

```css
div {
  background: orange;
  height: 30px;
  width: 200px;
}

div:empty {
  background: yellow;
}
```

**:enabled** é o inverso do `:disabled`. Por padrão, todos os elementos são habilitados.

</div>