<div align='justify'>

## Iniciando com NodeTS

>[youtube.com](https://youtu.be/uVB3NkrFIs8)
>
>25 março 2024

#### Passo 1: inicializar o npm

Digitar na prompt:
```
npm init
```

Pronto, um arquivo `package.json` foi criando. Este arquivo contém todas as dependências.

#### Passo 2: instalar o express e outras dependências essenciais 

Digitar na prompt:
```
npm install --save express pg drizzle-orm
```

Express é um microframework web feito para criar APIs REST. pg e drizzle-orm são bibliotecas utilizadas para manipulação de entidades no postgres.

O `--save` permite que as dependências sejam salvas no arquivo package.json.



#### Passo 3: instalar dependências de desenvolvimento.

Digitar na prompt:
```
npm install --save-dev typescript @types/express @types/node @types/pg drizzle-kit tsup tsx @faker-js/faker
```

Essas são dependências que só importam na hora de desenvolver, irrelevantes para a execução do programa.

#### Passo 4: Alterando o arquivo package.json

Dentro do arquivo package.json, na parte de scripts, inserir:

```json
"scripts":{
    "start": "tsx src/index.ts",
    "start:dev": "tsx --watch src/index.ts",
    "build": "tsup src/index.ts --format cjs,esm --dts --minify"
}
```

</div>