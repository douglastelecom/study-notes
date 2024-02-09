<div align='justify'>

## MÓDULOS NO ANGULAR

>[angular.io](https://angular.io/api/forms/NgModel)
>
>08 Fevereiro 2024

#### NGMODULE

O NgModule são arquivos que servem para agrupar todos os módulos que serão utilizados em um ou mais componentes.

```ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
@NgModule({
  imports:      [ BrowserModule ],\\quais módulos serão importados
  providers:    [ Logger ], \\serviços a serem injetados
  declarations: [ AppComponent ],\\quais componentes e diretivas pertencem
  exports:      [ AppComponent ], \\ser usado por outros componentes
  bootstrap:    [ AppComponent ] \\o módulo raiz
})
export class AppModule { }
```
Além de NgModules, os módulos podem ser importados diretamente dentro de seus respectivos componentes (não necessário se já está no NgModule), da seguinte forma:

```ts
import { Component } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
@Component({
 selector: 'app-root',
 templateUrl: './app.component.html',
 styleUrls: ['./app.component.sass']
 Imports: [BrowserModule]
})
export class AppComponent {}
```
Para importar tudo dentro de um componente e não utilizar nenhum NgModule associado, é necessário declarar o componente como standalone “standalone: true”.

#### COMO IMPORTAR MÓDULOS NO ANGULAR (EM NGMODULES OU COMPONENTES)

A importação padrão de módulos do js (ES2015) se dá da seguinte forma:
```ts
import { BrowserModule } from '@angular/platform-browser';
```

No entanto, apenas ela não é suficiente para importar componentes , pipes, diretivas e NgModules do angular. Para importar essas categorias dentro de um componente (ou NgModule), é necessário além da importação normal do JS, inserir o módulo dentro do array de imports no decorator:

```ts
@Component({
 selector: 'app-root',
 templateUrl: './app.component.html',
 styleUrls: ['./app.component.sass']
 Imports: [BrowserModule]
})
```

ou

```ts
@NgModule({
  imports:      [ BrowserModule ],
  providers:    [ Logger ],
  declarations: [ AppComponent ],
  exports:      [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
```
</div>