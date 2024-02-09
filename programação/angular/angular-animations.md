<div align='justify'>

## ANGULAR ANIMATIONS

>[Angular.io](https://angular.io/guide/animations)
>
>09 Fevereiro 2024

#### IMPORTAÇÃO

Para usar animação nos seus componentes `standalone`, é necessário importá-lo também no bootstrap da aplicação. Isso porque alguns módulos do angular afetam o projeto como um todo e precisam ser importados em um contexto mais global.

```ts
bootstrapApplication(AppComponent, {
  providers: [
    provideAnimations(),
  ]
});
```

Para aplicações que usam `ngModule`, você pode importar da seguinte maneira:

```ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';

@NgModule({
  imports: [
    BrowserModule,
    BrowserAnimationsModule
  ],
  declarations: [ ],
  bootstrap: [ ]
})
export class AppModule { }
```

Para importar a animação no componente, primeiro faça o import normal do js

```ts
import { Component, HostBinding } from '@angular/core';
import {trigger,state,style,animate,transition} from '@angular/animations';
```

Em seguida importe as animações dentro do espaço `animations`:
```ts
@Component({
  standalone: true,
  selector: 'app-root',
  templateUrl: 'app.component.html',
  styleUrls: ['app.component.css'],
  imports: [RouterLink, RouterOutlet],
  animations: [
    // animation triggers go here
  ]
})
```
#### ESTADOS E ESTILOS

A função state() serve para definir os estados do seu componente, ou seja, a aparência em cada estado. Por exemplo, um mesmo botão pode ter um comportamento “aberto” ou “fechado” e o state define como eles parecerão em cada um desses estados. Veja:

```ts
// ...
state('open', style({
  height: '200px',
  opacity: 1,
  backgroundColor: 'yellow'
})),
```
```ts
state('closed', style({
  height: '100px',
  opacity: 0.8,
  backgroundColor: 'blue'
})),
```
#### TRANSIÇÃO

Você pode mudar os estados dos componentes de forma abrupta. Isso geralmente não é recomendado, pois vai deixa as animações feias e sem sentido. Para transicionar as animações, use a função `transition`.

Em conjunto com o transition, você pode utilizar a função `animation()` para definir o tempo, delay e a aceleração da animação.

```ts
animate ('duration delay easing')
```
ou apenas
```ts
animate ('duration')
```
Dessa forma, utilizando a função transition ficamos com:
```ts
transition('open => closed', [
  animate('1s')
]),
```

#### TRIGGERING

Para criar uma animação é necessário a função `trigger()`. Ela será responsável por agrupar todas os estados, transições e animações e dar um nome. Veja o exemplo abaixo:

```ts
@Component({
  standalone: true,
  selector: 'app-open-close',
  animations: [
    trigger('openClose', [
      // ...
      state('open', style({
        height: '200px',
        opacity: 1,
        backgroundColor: 'yellow'
      })),
      state('closed', style({
        height: '100px',
        opacity: 0.8,
        backgroundColor: 'blue'
      })),
      transition('open => closed', [
        animate('1s')
      ]),
      transition('closed => open', [
        animate('0.5s')
      ]),
    ]),
  ],
  templateUrl: 'open-close.component.html',
  styleUrls: ['open-close.component.css']
})
export class OpenCloseComponent {
  isOpen = true;

  toggle() {
    this.isOpen = !this.isOpen;
  }

}
```

Devemos então associar o nosso trigger openClose à um elemento específico. Podemos fazer isso da seguinte forma:

```html
<div [@triggerName]="expression">…</div>;
```

Assim, sempre que a variável `expression` muda de valor (estado), a animação acontece. Veja um exemplo real:

```html
<nav>
  <button type="button" (click)="toggle()">Toggle Open/Close</button>
</nav>

<div [@openClose]="isOpen ? 'open' : 'closed'" class="open-close-container">
  <p>The box is now {{ isOpen ? 'Open' : 'Closed' }}!</p>
</div>
```
A função `toggle()` muda o valor de `isOpen`, atribuindo um estado `open` ou `close` à `@openClose`.

```ts
  toggle() {
    this.isOpen = !this.isOpen;
  }
```



</div>