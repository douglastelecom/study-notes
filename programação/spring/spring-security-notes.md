<div align='justify'>

## TÍTULO 1

>[youtube.com](https://youtu.be/5w-YCcOjPD0)
>
>16 Maio de 2024

#### Preparando o POM

Assim que você insere as bibliotecas do spring security *"spring-boot-starter-security"* e *"spring-security-test"* os endpoints da sua aplicação já serão automaticamente protegidos, retornando *"unauthorized"*. Para fazer qualquer solicitação ele pede para o usuário fazer uma autenticação.

Quando a aplicação é iniciada, o spring-security gera um password que pode ser encontrado nos logs da aplicação. O usuário é *"user"*.

#### Criação da arquitetura padrão

A tabela do postgres não pode se chamar "user", pois é uma palavra reservada para ele. Por isso, devemos criar uma tabela com o nome "users", no plural.

Você deve criar uma classe chamada "User", que implementa a UserDetails (e implementar seus métodos)

Criar uma enum com as roles ("admin", "user" etc)

Depois criar um repository `UserRepository` e criar um método `findByLogin()` que retorna um `UserDetails`.

Criar um service `AuthorizationService` que implementa o `UserDetailsService` e através de um método `loadUserByUsername(String username)` retorna a consulta do findByLongin(String username) do `UserRepository`.

#### Desativar as configurações padrões do spring security

Criar uma classe chamada `securityConfigurations` e utilizar as notações `@Configuration` e `@EnableWebSecurity`.

Imeplementar o método SecurityFilterChain() e configurar o spring security.

#### Controle de autenticação





![alt text](image.png)

</div>