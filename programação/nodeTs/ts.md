<div align='justify'>

## TS

>[youtube.com](https://youtu.be/XuTfN_84rcU)
>
>25 Março 2024

#### O que é o TS?

O typescript é uma linguagem que possibilita usar tipagem estática em JS, que é naturalmente de tipagem dinâmica. Isso diminuir a quantidade de erros em tempo de execução e possibilita um melhor intellisense da IDE. Todo o código em TS é convertido para JS.

#### Type vs Interface

Os dois são praticamente iguais, exceto que uma classe não pode implementar um `type`, apenas um `interface`.

```ts
interface User{
    name?: string
    age: number
    address: Adress
}
```
ou
```ts
type User{
    name?: string
    age: number
    address: Adress
}
```

#### Keyof

O keyof é um utilitário do typescript capaz de transformar os atributos de uma interface em uma enum. Por exemplo, veja o código abaixo:

```ts

type User{
    name?: string
    age: number
    address: Adress
}

type usuarioPropriedades = keyof User

```

O tipo `usuarioPropriedades` é um enum dos tipos de `User`.

```ts
function pickProperty(user: User, property: UserProperties){
    return user[property]
}
```

O parâmetro `property` só pode ser três valores de string: "name", "age" ou "address". Qualquer outro valor além desses resulta em um erro.

#### Typeof

O typeof é um utilitário que cria um tipo a partir de um objeto. Por exemplo:

```ts
const video = {
    title: "usando Typescript",
    duration: 180
}

type Video = typeof video

```

Dessa forma `Video` será um tipo que possui os campos `title: string` e `duration: number`.

É possível utilizar os dois utilitários, `keyof` e `typeof`, em conjunto:

```ts
type Video = keyof typeof video
```

Assim video será uma espécie de enum que apenas permite os valores "title" ou "duration".

</div>