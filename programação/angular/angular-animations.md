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

Você pode mudar os estados dos componentes de forma abrupta. Isso geralmente não é recomendado, pois vai deixa as animações feias e sem sentido. Para transicionar as animações, use a função transition.



</div>