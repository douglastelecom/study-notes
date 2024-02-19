<div align='justify'>

## PSEUDOCLASSES E PSEUDOELEMENTS

>[smashingmagazine.com](https://www.smashingmagazine.com/2016/05/an-ultimate-guide-to-css-pseudo-classes-and-pseudo-elements/)
>
>16 Fevereiro 2024

#### SIMBOLOGIA

Pseudoclasses e pseudoelements são diferentes. Pseudoclasse se refere à um estado, enquanto o pseudolemento se refere a algum elemento acessório do elemento principal (que poderá ser tratado como um elemento html). As pseudoclasses são representadas com `:`, por exemplo `div:hover{}`, e os pseudoelementos são representados com `::`, por exemplo `div::after{}`.

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

**:in-range** tem como alvo elementos que possuem um intervalo. Veja o exemplo abaixo, o estilo css será ativado apenas quando o tamanho do input estiver dentro de 5 e 10.

```html
<input type="number" min="5" max="10">
```

```css
input[type=number] {
    border: 5px solid orange;
}

input[type=number]:in-range {
    border: 5px solid green;
}
```

**:out-of-range** é muito semelhante ao `:in-range`, mas funciona de forma inversa.

**:indeterminate** é ativado em checkboxs ou radiobuttons. Por exemplo, quando nenhum botão de um radiobutton é selecionado, ele fica no estado de indeterminação.

```html
<ul>
    <li>
        <input type="radio" name="list" id="option1">
        <label for="option1">Option 1</label>
    </li>
    <li>
        <input type="radio" name="list" id="option2">
        <label for="option2">Option 2</label>
    </li>
    <li>
        <input type="radio" name="list" id="option3">
        <label for="option3">Option 3</label>
    </li>
</ul>
```

```css
:indeterminate + label {
    background: orange;
}
```

**:valid** tem como alvo elementos cuja formatação está correta de acordo com o formato exigido.

```css
input[type=email]:valid {
    border: 1px solid green;
}
```

**:invalid** é o inverso de `:valid`.

**:optional** tem como alvo campos de entrada que não são obrigatórios. Em outras palavras, que não possuam `required`.

```html
<input type="number">
```

```css
:optional {
    color: gray;
}
```

**:read-only** ativado apenas quando o elemento possui o atributo `readonly`.

```html
<input type="text" value="I am read only" readonly>
```

```css
input:read-only {
    color: gray;
}
```

**:read-write** tem como alvo os elementos que podem ser editados pelo usuário. Também pode ser ativado em elementos que possuem o atributo `contenteditable`. O exemplo a seguir combina o `:read-write` com o `focus`.

```html
<div class="editable" contenteditable>
    <h1>Click on this text to edit it</h1>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit!</p>
</div>
```

```css
:read-write:focus {
    padding: 5px;
    border: 1px dotted black;
}
```

**:required** é semelhante ao `read-only`, porém funciona de forma inversa. Só ativa em elementos com o atributo `required`

**:scope (experimental)** só faz sentido quando vinculado ao atributo `scoped` em uma tag `style` dentro de um arquivo html. No exemplo abaixo, apenas o segundo `section` ficará em itálico.

```html
<article>
    <section>
        <h1>Lorem ipsum dolor sit amet</h1>
        <p>Lorem ipsum dolor sit amet.</p>
    </section>
    <section>
        <style scoped>
                        :scope {
                            font-style: italic;
                        }
                  </style>
        <h1>This text will be italicized</h1>
        <p>This text will be italicized.</p>
    </section>
</article>
```

**:dir (experimental)** basicamente seleciona as tagas que funcionam da esquerda para a direita, ou da direita para a esquerda. O exemplo abaixo está escrito em árabe, cuja leitura se dá da direita para a esquerda.

```html
<article dir="rtl">
    <p>التدليك واحد من أقدم العلوم الصحية التي عرفها الانسان والذي يتم استخدامه لأغراض الشفاء منذ ولاده الطفل.</p>
</article>
```
```css
/* unprefixed */
article :dir(rtl) {
    color: orange;
}
```
**:lang** corresponde à linguagem do idioma.

```html
<article lang="en">
    <q>Lorem ipsum dolor sit amet.</q>
</article>
<article lang="fr">
    <q>Lorem ipsum dolor sit amet.</q>
</article>
<article lang="de">
    <q>Lorem ipsum dolor sit amet.</q>
</article>
```

```css
:lang(en) q { quotes: '“' '”'; }
:lang(fr) q { quotes: '«' '»'; }
:lang(de) q { quotes: '»' '«'; }
```

##### DIVERSOS

Vamos agora ver pseudoclassses com outras funcionalidades.

**:root** refere-se ao elemento mais alto em um documento. Geralmente o elemento `html`.

```css
:root {
    background: orange;
}
```

**:fullscreen (experimental)** tem como alvo elementos exibidos em fullscreen. Porém, não funciona quando o usuário pressiona f11, mas em APIs JavaScript Fullscreen, voltadas para imagens, vídeos e jogos executados em um contêiner pai.

```html
<h1 id="element">This heading will have a solid background color in full-screen mode.</h1>
<button onclick="var el = document.getElementById('element'); el.webkitRequestFullscreen();">Trigger full screen!</button>
```

```css
h1:fullscreen {
    background: orange;
}
```

#### PSEUDOELEMENTOS

Elementos que não estão representados no DOM, pois não os digitamos em html, mas os criamos no CSS. Os pseudoelementos são usados para adicionar estilos a partes específicas do conteúdo de um elemento, como o primeiro caractere de um parágrafo.

**::before** adiciona outro elemento html antes do elemento. O conteúdo não está na DOM, mas pode ser manipulado como se estivesse. E a propriedade `content` precisa ser declarada no css. É possível também inserir uma tag <span> em content.

```html
<h1>Ricardo</h1>
```

```css
h1:before {
    content: "Hello "; /* Note the space after the word Hello. */
}
```

Será renderizado como: Hello Ricardo!

**::after** faz o mesmo que before, porém depois.

**::backdrop (experimental)** é uma caixa gerada atrás do elemento de tela inteira, mas que fica acima de todos os outros conteúdos.
**::first-letter** seleciona a primeira letra de uma linha de texto.

```css
h1:first-letter  {
    font-size: 5em;
}
```

**::first-line** é muito parecido com first-letter, mas em vez da primeira letra, seleciona a primeira linha.

```css
p:first-line {
    background: orange;
}
```

**::select** altera a aparência do texto selecionado.

```css
::selection  {
    color: orange;
    background: #333;
}
```

**::placeholder** tem como alvo o texto de placeholder em um input.

```html
<input type="email" placeholder="name@domain.com">
```

```css
input::placeholder {
    color:#666;
}
```

</div>