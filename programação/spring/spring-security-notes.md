<div align='justify'>

## Spring Security com Auth0 (JWT)

>[medium.com](https://medium.com/@felipeacelinoo/protegendo-sua-api-rest-com-spring-security-e-autenticando-usu%C3%A1rios-com-token-jwt-em-uma-aplica%C3%A7%C3%A3o-d70e5b0331f9)
>
>16 Maio de 2024

#### Classe User

Representa o usuário da aplicação. Contem informações de login e outros atributos inerentes ao usuário da aplicação.

#### Classe UserRepository

É a classe responsável por recuperar um User do banco de dados a partir do seu login.

#### Interface UserDetails

Normalmente se implementa essa interface em uma classe a parte `UserDetailsImpl` que conterá apenas as informações pertinentes ao login e autenticação de usuário, como `login` e `password`.

#### Interface UserDetailsService

Serve apenas para retornarmos um `UserDetailImpl` a partir dos dados de um `User` normal.

#### Classe JwtTokenService

Responsável por gerar o token da aplicação, e também para recuperar um `userName`/`login` a partir desse token.

#### Classe UserAuthenticationFilter

Verifica se o usuário é válido e autentica-o. Utiliza as classes descritas anteriormente `JwtTokenService` e `UserRepository` para essa função.

#### Classe SecurityConfiguration

Essa é a classe de configuração do Spring Security. Aqui é definido quais paths precisarão de autenticação e qual será o filtro utilizado para recuperar os dados do token, nesse caso o filtro descrito anteriormente `UserAuthenticationFilter`.

#### Classe UserController

Responsável por receber as requisições de login ou autenticação do usuário. Encaminha tudo para o `UserService`.

#### Classe UserService

O `UserService` irá autenticar o usuário e retornar um token. Também é responsável por cadastrar novos usuários. 

## Fluxo

A requisição de login chega em `UserController`, que contata a classe `UserService` que irá autenticar e retornar um token através da classe `JwtTokenService`.

Depois todas as requisições feitas pelo frontend conterão esse token retornado, possibilitando que o usuário possa fazer requisições aos outros paths do sistema.

</div>