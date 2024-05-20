<div align='justify'>

## TÍTULO 1

>[youtube.com](https://youtu.be/5w-YCcOjPD0)
>
>16 Maio de 2024

### Preparando o POM

Assim que você insere as bibliotecas do spring security *"spring-boot-starter-security"* e *"spring-security-test"* os endpoints da sua aplicação já serão automaticamente protegidos, retornando *"unauthorized"*. Para fazer qualquer solicitação ele pede para o usuário fazer uma autenticação.

Quando a aplicação é iniciada, o spring-security gera um password que pode ser encontrado nos logs da aplicação. O usuário é *"user"*.

### Criação da arquitetura padrão

A tabela do postgres não pode se chamar "user", pois é uma palavra reservada para ele. Por isso, devemos criar uma tabela com o nome "users", no plural.

Você deve criar uma classe chamada "User", que implementa a UserDetails (e implementar seus métodos)

Criar uma enum com as roles ("admin", "user" etc)

Depois criar um repository `UserRepository` e criar um método `findByLogin()` que retorna um `UserDetails`.

Criar um service `AuthorizationService` que implementa o `UserDetailsService` e através de um método `loadUserByUsername(String username)` retorna a consulta do findByLongin(String username) do `UserRepository`.

### Desativar as configurações padrões do spring security

Criar uma classe chamada `securityConfigurations` e utilizar as notações `@Configuration` e `@EnableWebSecurity`.

Criar um bean `SecurityFilterChain()` com @bean e configurar o spring security.

### Controle de autenticação

No método `SecurityFilterChain()` criado anteriormente, deve-se definir os paths que precisarão de autenticação.

### Endpoint de autenticação

Criar uma classe `AuthenticationController`

Criar uma entidade `AuthenticationDTO`, contendo login e senha.

Criar um método `login()` no `AuthenticationController`. O método `login()` recebe o login e o password.

Criar um novo bean `AuthenticationManager` dentro da classe `SecurityConfigurations` que será responsável pela autenticação do usuário.

### Criar um hash da senha

Ainda na classe `SecurityConfigurations` é necessário criar um bean chamado `PasswordEncoder()` que será responsável por criptografar a senha do usuário.

### Registrar novos usuários

Criar um método register dentro de `AuthenticatioinController`

### JWT

Instalar a dependência do JWT para java.

Criar uma classe TokenService e após isso atribuir o método `generateToken()`, `genExpirationDate()` e `validateToken()`

### Alterando as configurações de segurança

No método `securityFilterChain()`, da classe `SecurityConfigurations`, adicionar um filtro que verifica a autorização e a role do usuário.

Criar a classe `SecurityFilter` que extende a classe `OncePerRequestFilter`

### Retornando token para o usuário

Em `AuthenticationController` importar o `TokenService` e adicionar no método `login()` um retorno do token para a requisição.





![alt text](image.png)

</div>