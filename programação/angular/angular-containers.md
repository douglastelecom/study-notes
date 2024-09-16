<div align='justify'>

## ANGULAR CONTAINERS

>[freecodecamp.org](https://www.freecodecamp.org/portuguese/news/tudo-o-que-voce-precisa-saber-sobre-ng-template-ng-content-ng-container-e-ngtemplateoutlet-em-angular/)
>[angular.io](https://angular.io/api/core/ng-container)
>
>21 Fevereiro 2024

#### ng-template

Como o nome sugere, é um elemento de template que o Angular usa com as diretivas estruturais (`*ngIf`, `*ngFor`, `[ngSwitch]` e as diretivas personalizadas).

Observe o código abaixo. Sempre que você usa uma diretiva, o angular interpreta-a encapsulando seu elemento dentro de um `<ng-template>`.

![teste](/assets/images/angular/angular-containers/1.png)

A forma final renderizada é a seguinte:

![teste](/assets/images/angular/angular-containers/2.jpeg)

Mas para onde foi o `<ng-template>`? Na verdade, ele não é renderizado como um elemento html, o angular apenas adiciona códigos de diagnóstico para indicar que existe um código TS por trás dos panos para renderizar aqueles componentes filhos (nesse caso, a `<div>`).

Já entendemos que o angular usa o `<ng-template>` para interpretar diretivas estruturais, mas e se quisermos utilizar o `<ng-template>` diretamente? Bom, primeiro é necessário ter uma diretiva estrutural (pois eles só funcionam com elas), como o *ngIf.

![teste](/assets/images/angular/angular-containers/3.png)

Isso seria renderizado como:

![teste](/assets/images/angular/angular-containers/4.jpeg)

O angular apenas inseriu comentários de diagnóstico dentro de outro comentário de diagnóstico. Isso porque o *ngIF fez o angular criar outro `<ng-template>` para encapsular o próprio `<ng-template>`, e isso está errado.

Existem dois métodos corretos para usar um `<ng-template>`. Veja:

![teste](/assets/images/angular/angular-containers/7.png)

O primeiro método é o sem rodeios, assim o angular apenas converte o `<ng-template>` em comentários e mantém o conteúdo dentro dele intocado.

O segundo método é raramente utilizado com dois `<ng-template>`, mas é comumente utilizado combinando uma tag `<ng-template>` com uma tag `<ng-container>`. Damos uma referência de template a *ngIf em seu then para informar a ele qual template deve ser usado se a condição for verdadeira, o primeiro `<ng-template>` invoca o segundo `<ng-template>` caso a condição seja verdadeira.

#### ng-container

Você já viu ou escreveu algum código assim:

![teste](/assets/images/angular/angular-containers/8.png)

Isso acontece porque o angular não permite mais de uma diretiva em um único componente. Se permitisse, poderíamos ter usado apenas uma única `<div>` com as duas diretivas, `*ngIf` e `*ngFor`.

O código acima funciona, porém enche a DOM com divs vazias (caso item.id seja falso). Veja

![teste](/assets/images/angular/angular-containers/9.jpeg)

Isso pode representar um problema em DOMs complexas ezibindo dezenas de milhares de dados.

Mas sem problemas, para isso existe o `<ng-container>`. É um elemento de agrupamento que não interfere no layout, pois não é adicionado ao DOM.

Assim, poderíamos ter escrito o código anterior da seguinte forma:

![teste](/assets/images/angular/angular-containers/10.png)

E o DOM final seria (perceba que as divs sumiram).

![teste](/assets/images/angular/angular-containers/11.jpeg)

O `<ng-container>` é muito importante quando queremos utilizar diretivas estruturais sem intoruzir elementos extras na DOM.

Como dito no capítulo anterior, é possível utilizar o `<ng-container>` em conjunto com o `<ng-template>`:

```html
<ng-container *ngIf="condition; else templateA">
  …
</ng-container>
<ng-template #templateA>
  …
</ng-template>
```

Também é possível utilizar os dois em conjunto de uma outra forma, utilizando a diretiva `*ngTemplateOutlet`, mas veremos isso mais a frente, no capítulo dessa diretiva.

#### ng-content

Serve para inserir elementos html dentro de um componente. Por exemplo, observe o componente project-content abaixo. A div interna passada será invocada no footer, onde está o `<ng-content>`.

![teste](/assets/images/angular/angular-containers/13.png)
![teste](/assets/images/angular/angular-containers/12.png)

Também é possível utilizar projeções múltiplas, escolhendo em qual posição um elemento específico do `<ng-content>` deve ser renderizado:

![teste](/assets/images/angular/angular-containers/14.png)

O resto do conteúdo que não foi selecinoado será renderizado no último `<ng-content>`.

#### *ngTemplateOutlet

Ele pode ser utilizado para inserir um mesmo template em diversos lugares:

![teste](/assets/images/angular/angular-containers/16.png)

Ele também pode ser utilizado para criar componentes altamente personalizáveis. Veja o exemplo a seguir:

![teste](/assets/images/angular/angular-containers/17.png)

![teste](/assets/images/angular/angular-containers/18.png)

E os insere da seguinte forma:

![teste](/assets/images/angular/angular-containers/19.png)

#### ng-content x *ngTemplateOutlet

A vantagem de usar o *ngTemplateOutlet é que eles nos fornece a oportunidade de um template default, caso nenhum template seja inserido.

No entanto, o ng-content possui uma sintaxe mais simples. A escolha de um ou de outro vai depender totalmente do seu caso de uso.

</div>