<div align='justify'>

## POSITION E DISPLAY

>[medium.com](https://medium.com/@iagomachado/conhecendo-conceitos-b%C3%A1sicos-de-css-position-e-display-fe878eca0690)
>
>15 Fevereiro 2024

#### DISPLAY

Define como o bloco de um componente será renderizado na tela.

Observe a figura abaixo.

![html-display](/assets/images/position-and-display/position-and-display-1.webp)

Perceba que os links renderizaram lado a lado.

![html-display](/assets/images/position-and-display/position-and-display-2.webp)

Por que isso acontece? Porque as tags `<a>` são definidas com o estilo `display: inline` por padrão. Elas renderizam uma ao lado da outra.

Se quisermos uma acima da outra, em coluna, precisamos mudar o display para `display: block`. Veja:

![html-display](/assets/images/position-and-display/position-and-display-3.webp)

![html-display](/assets/images/position-and-display/position-and-display-4.webp)

- **Display Block:** Renderiza os elementos um abaixo do outro.

- **Display Inline:** Renderiza os elementos um ao lado do outro.

- **Display Inline-block:** Renderiza os elementos que podem se apresentar tanto em linha quanto em bloco, dependendo da largura disponível.

- **Display Flex:** Renderiza todos os elementos filhos dele como um flex-item (repare que é utilizado no pai). É muito utilizado quando queremos posicionar elementos dentro de um bloco pai, garantindo um posicionamento flexível vertifical ou horizontal desses elementos.
É o mais utilizado visto sua flexibilidade para posicionar elementos dentro de um container. Após sua implementação, muitas técnicas de alinhamento horizontal, como float position ou vertical-align caíram em desuso.

- **Display Grid:** O mais recente das propriedades do tipo display, permite a renderização de elementos posicionados em grids, garantindo assim flexibilidade para ciar seções de layout. É muito utilizado para construção de grids para interface como um todo.

#### POSIÇÃO

É a propriedade que mais confunde os desenvolvedores.

Para esta propriedade precisamos pensar na nossa tela como um plano cartesiano, no qual os pontos e x e y começam no topo esquerdo da tela.

![html-display](/assets/images/position-and-display/position-and-display-5.webp)

Existem cinco tipos de posições:

- **Static:** Valor padrão para qualquer elemento na página. Garante que ele seguirá o fluxo de renderização padrão atribuído pela propriedade display.

- **Relative:** Ao aplicar o tipo relative em um elemento, ele poderá ser manipulado através das propriedades top, bottom, left ou right. Cada um deles possui valores numéricos que determinam em qual coordenada x ou y seu elemento irá se mover.
Ao contrário do absolute, o relative leva em consideração apenar o posicionamento do seu elemento, desconsiderando a posição do elemento pai.

![html-display](/assets/images/position-and-display/position-and-display-6.webp)

![html-display](/assets/images/position-and-display/position-and-display-7.webp)

- **Absolute:** Ao contrário do relative, o absolute leva em consideração a posição do pai do elemento. Veja o exemplo abaixo:

![html-display](/assets/images/position-and-display/position-and-display-8.webp)

![html-display](/assets/images/position-and-display/position-and-display-9.webp)

![html-display](/assets/images/position-and-display/position-and-display-10.webp)

- **Fixed:** Se comporta de forma muito similar ao absolute, mas leva em consideração apenas a posição do elemento window/body. Não o pai do elemento. É um recurso que nos permite criar elementos fixos que independem do scroll da página.

![html-display](/assets/images/position-and-display/position-and-display-11.webp)

![html-display](/assets/images/position-and-display/position-and-display-12.webp)

![html-display](/assets/images/position-and-display/position-and-display-13.webp)

- **Sticky:** Permite que um elemento hora funcione como relative e outras vezes como fixed. Muito utilizado para menus que são fixos e ao mesmo tempo relativos quando necessário.

![html-display](/assets/images/position-and-display/position-and-display-14.gif)

</div>