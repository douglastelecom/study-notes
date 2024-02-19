<div align='justify'>

## SASS

>[sass-lang.com](https://sass-lang.com/guide/#variables)
>
>12 Fevereiro 2024

#### PRÉ-PROCESSAMENTO

CSS é útil, mas possui limitações que tornam a manutenção de estilos complexa. Um pré-processamento pode ajudar com essas limitações. Sass possui  funções que não existem em css, como nesting, mixins, inheritace, além de outras funcionalidades, e sempre converte o código final em css para poder ser usado no seu site.

#### VARIÁVEIS

As variáveis servem para armazenar informações que você irá reutilizar no seu estilo. Sass usa o símbolo $ para fazer de uma palavra uma variável. Veja o exemplo abaixo:
```scss
$font-stack: Helvetica, sans-serif
$primary-color: #333

body
  font: 100% $font-stack
  color: $primary-color
```

#### ANINHAMENTO (NESTING)

O CSS não possui um aninhamento muito claro de seus elementos, como o HTML. O Sass permite que o aninhamento aconteça de forma clara e simples, sem repetição de código:

```scss
nav
  ul
    margin: 0
    padding: 0
    list-style: none

  li
    display: inline-block

  a
    display: block
    padding: 6px 12px
    text-decoration: none
```

Agora veja o mesmo código em css:`

```css
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
nav li {
  display: inline-block;
}
nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```

É uma forma muito boa de organizar o seu código.

#### PARCIAIS (PARTIALS)

Arquivos parciais servem para armazenar código que não será compilado em css. O "_" (underline) serve para informar ao Sass que o arquvio não precisa ser transformado em css. Exemplo `_partial.sass`. Para importá-lo use a anotação @use (se for dart sass), ou o @import. Não hora de usar o @use, não é necessário utilizar o "_"(underline).

```scss
// _base.sass
$font-stack: Helvetica, sans-serif
$primary-color: #333

body
  font: 100% $font-stack
  color: $primary-color
```

```scss
// styles.sass
@use 'base' 
//(ou @import "./assets/styles/_base.sass")

.inverse
  background-color: base.$primary-color
  color: white

```

Isso seria o equivalente a:

```css
body {
  font: 100% Helvetica, sans-serif;
  color: #333;
}

.inverse {
  background-color: #333;
  color: white;
}
```

#### MISTURAS (MIXINS)

Algumas coisas no css são tediosas e repetitivas para escrever. Dessa forma você pode reaproveitar e tornar o seu código mais enxuto da seguinte forma:

```scss
@mixin theme($theme: DarkGray)
  background: $theme
  box-shadow: 0 0 1px rgba($theme, .25)
  color: #fff

.info
  @include theme

.alert
  @include theme($theme: DarkRed)

.success
  @include theme($theme: DarkGreen)
```

Em css isso resultaria em:

```css
.info {
  background: DarkGray;
  box-shadow: 0 0 1px rgba(169, 169, 169, 0.25);
  color: #fff;
}

.alert {
  background: DarkRed;
  box-shadow: 0 0 1px rgba(139, 0, 0, 0.25);
  color: #fff;
}

.success {
  background: DarkGreen;
  box-shadow: 0 0 1px rgba(0, 100, 0, 0.25);
  color: #fff;
}
```

Os mixins nada mais são do que um tipo especial de funções css que recebem parâmetros e retornam código css. Não confundir com as funções normais do css que retornam números ou strings.

#### ESTENDER (EXTEND) E HERANÇA (INHERITANCE)

Você pode herdar um conjunto de propriedades sass da seguinte forma:

```scss
/* This CSS will print because %message-shared is extended. */
%message-shared
  border: 1px solid #ccc
  padding: 10px
  color: #333

// This CSS won't print because %equal-heights is never extended.
%equal-heights
  display: flex
  flex-wrap: wrap

.message
  @extend %message-shared

.success
  @extend %message-shared
  border-color: green

.error
  @extend %message-shared
  border-color: red

.warning
  @extend %message-shared
  border-color: yellow
```

#### OPERADORES E FUNÇÕES

É possível utilizar operadores matemáticos em sass.

```scss
@function fibonacci($n)
  $sequence: 0 1
  @for $_ from 1 through $n
    $new: nth($sequence, length($sequence)) + nth($sequence, length($sequence) - 1)
    $sequence: append($sequence, $new)
  @return nth($sequence, length($sequence))

.sidebar
  float: left
  margin-left: fibonacci(4) * 1px
```

</div>

#### MAPAS ANINHADOS

Ao invés de digitar várias variáveis de um mesmo grupo, você pode escrever maps:

Ao invés disso:

```scss
$bg: #242943
$bg-alt: #2a2f4a
$fg: #ffffff
```

Você pode fazer isso:

```scss
$palette: ("bg":#242943, "bg-alt":#2a2f4a, "fg":#ffffff) //é importante que fiquem em linha
```

E resgatar a cor da seguinte forma:

```scss
@use "sass:map"
@import "./assets/styles/_vars.sass"
body
    background-color: map.get($palette, bg)
```