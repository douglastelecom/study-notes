<div align='justify'>

## TÍTULO 1

>[youtube.com](https://youtu.be/5w-YCcOjPD0)
>
>16 Maio de 2024

### Preparando o POM

Assim que você insere as bibliotecas *"spring-boot-starter-security"*, *"spring-security-test"* e *"auth0"* os endpoints da sua aplicação já serão automaticamente protegidos, retornando *"unauthorized"*. Para fazer qualquer solicitação ele pede para o usuário fazer uma autenticação.

```xml
    <dependencies>
		<dependency>
			<groupId>com.auth0</groupId>
			<artifactId>java-jwt</artifactId>
			<version>4.4.0</version>
		</dependency>
        		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-security</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.security</groupId>
			<artifactId>spring-security-test</artifactId>
			<scope>test</scope>
		</dependency>
    </dependencies>
```

Quando a aplicação é iniciada, o spring-security gera um password que pode ser encontrado nos logs da aplicação. O usuário é *"user"*.

### Criação da arquitetura padrão

Criar uma enum com as roles ("admin", "user" etc)

A tabela do postgres não pode se chamar "user", pois é uma palavra reservada para ele. Por isso, devemos criar uma tabela com o nome "users", no plural.

Você deve criar uma classe chamada "User", que implementa a UserDetails (e implementar seus métodos)


```java
package parnamirim.rn.gov.br.semsur.entity;
import com.fasterxml.jackson.annotation.JsonProperty;
import jakarta.persistence.*;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;
import org.springframework.security.core.GrantedAuthority;
import org.springframework.security.core.authority.SimpleGrantedAuthority;
import org.springframework.security.core.userdetails.UserDetails;
import parnamirim.rn.gov.br.semsur.enumerated.UserRole;
import java.util.Collection;
import java.util.List;

@Data
@Entity
@Table(schema = "usuarios", name = "usuario")
@NoArgsConstructor
@AllArgsConstructor
public class User implements UserDetails {

    public User(String login, String password, UserRole role) {
        this.login = login;
        this.password = password;
        this.role = role;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Integer id;

    @Column(name = "login")
    private String login;

    @Column(name = "senha")
    @JsonProperty(access = JsonProperty.Access.WRITE_ONLY)
    private String password;

    @Enumerated(EnumType.STRING)
    private UserRole role;

    @Override
    public Collection<? extends GrantedAuthority> getAuthorities() {
        if (this.role == UserRole.ADMIN)
            return List.of(new SimpleGrantedAuthority("ROLE_ADMIN"), new SimpleGrantedAuthority("ROLE_USER"));
        else
            return List.of(new SimpleGrantedAuthority("ROLE_USER"));
    }

    @Override
    public String getUsername() {
        return login;
    }

    @Override
    public String getPassword() {
        return password;
    }

    @Override
    public boolean isAccountNonExpired() {
        return true;
    }

    @Override
    public boolean isAccountNonLocked() {
        return true;
    }

    @Override
    public boolean isCredentialsNonExpired() {
        return true;
    }

    @Override
    public boolean isEnabled() {
        return true;
    }
}

```

Depois criar um repository `UserRepository` e criar um método `findByLogin()` que retorna um `UserDetails`.
```java
package com.example.auth.repositories;
import com.example.auth.domain.user.User;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.security.core.userdetails.UserDetails;

public interface UserRepository extends JpaRepository<User, Integer> {
    UserDetails findByLogin(String login);
}
```
Criar um service `AuthorizationService` que implementa o `UserDetailsService` e através de um método `loadUserByUsername(String username)` retorna a consulta do findByLongin(String username) do `UserRepository`.
```java
package parnamirim.rn.gov.br.semsur.security.services;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.core.userdetails.UsernameNotFoundException;
import org.springframework.stereotype.Service;
import parnamirim.rn.gov.br.semsur.repository.UserRepository;

@Service
public class AuthotizationService implements UserDetailsService{
    
    @Autowired
    UserRepository repository;

    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        return repository.findByLogin(username);
    }
}
```

### Configurando a criação e validação do token JWT

Criar uma classe chamada `JwtTokenService` com os métodos necessários para gerar um token e recuperar um usuário a partir do token.

```java
@Service
public class JwtTokenService {

    @Value("${api.security.token.secret}")
    private String secret; // Chave secreta utilizada para gerar e verificar o token 

    private String issuer = "minha-api"; // Emissor do token

    public String generateToken(User user) {
        try {
            // Define o algoritmo HMAC SHA256 para criar a assinatura do token passando a chave secreta definida
            Algorithm algorithm = Algorithm.HMAC256(secret);
            return JWT.create()
                    .withissuer(issuer) // Define o emissor do token
                    .withIssuedAt(creationDate()) // Define a data de emissão do token
                    .withExpiresAt(expirationDate()) // Define a data de expiração do token
                    .withSubject(user.getUsername()) // Define o assunto do token (neste caso, o nome de usuário)
                    .sign(algorithm); // Assina o token usando o algoritmo especificado
        } catch (JWTCreationException exception){
            throw new JWTCreationException("Erro ao gerar token.", exception);
        }
    }

    public String getSubjectFromToken(String token) {
        try {
            // Define o algoritmo HMAC SHA256 para verificar a assinatura do token passando a chave secreta definida
            Algorithm algorithm = Algorithm.HMAC256(secret);
            return JWT.require(algorithm)
                    .withissuer(issuer) // Define o emissor do token
                    .build()
                    .verify(token) // Verifica a validade do token
                    .getSubject(); // Obtém o assunto (neste caso, o nome de usuário) do token
        } catch (JWTVerificationException exception){
            throw new JWTVerificationException("Token inválido ou expirado.");
        }
    }

    private Instant creationDate() {
        return ZonedDateTime.now(ZoneId.of("America/Recife")).toInstant();
    }

    private Instant expirationDate() {
        return ZonedDateTime.now(ZoneId.of("America/Recife")).plusHours(4).toInstant();
    }

}
```

Lembrar de adicionar dentro do arquivo *"pom.xml"* `api.security.token.secret=${JWT_SECRET:4Z^XrroxR@dWxqf$mTTKwW$!@#qGr4P}`.

### Criando um filtro de segurança

Agora nós iremos criar um filtro personalizado para verificar se o usuário é um usuário válido e autenticá-lo. O filtro usará o `UserRepository` e `JwtTokenService` que implementamos para encontrar e verificar se o usuário é válido e autenticá-lo.

```java
@Component
public class UserAuthenticationFilter extends OncePerRequestFilter {

    @Autowired
    private JwtTokenService jwtTokenService; // Service que definimos anteriormente

    @Autowired
    private UserRepository userRepository; // Repository que definimos anteriormente

    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain filterChain) throws ServletException, IOException {
        // Verifica se o endpoint requer autenticação antes de processar a requisição
        if (checkIfEndpointIsNotPublic(request)) {
            String token = recoveryToken(request); // Recupera o token do cabeçalho Authorization da requisição
            if (token != null) {
                String subject = jwtTokenService.getSubjectFromToken(token); // Obtém o assunto (neste caso, o nome de usuário) do token
                User user = userRepository.findByLogin(subject).get(); // Busca o usuário pelo email (que é o assunto do token)

                // Cria um objeto de autenticação do Spring Security
                Authentication authentication =
                        new UsernamePasswordAuthenticationToken(user.getUsername(), null, user.getAuthorities());

                // Define o objeto de autenticação no contexto de segurança do Spring Security
                SecurityContextHolder.getContext().setAuthentication(authentication);
            } else {
                throw new RuntimeException("O token está ausente.");
            }
        }
        filterChain.doFilter(request, response); // Continua o processamento da requisição
    }

    // Recupera o token do cabeçalho Authorization da requisição
    private String recoveryToken(HttpServletRequest request) {
        String authorizationHeader = request.getHeader("Authorization");
        if (authorizationHeader != null) {
            return authorizationHeader.replace("Bearer ", "");
        }
        return null;
    }

    // Verifica se o endpoint requer autenticação antes de processar a requisição
    private boolean checkIfEndpointIsNotPublic(HttpServletRequest request) {
        String requestURI = request.getRequestURI();
        return !Arrays.asList(SecurityConfiguration.ENDPOINTS_WITH_AUTHENTICATION_NOT_REQUIRED).contains(requestURI);
    }
}
```

### Definindo as demais configurações de segurança do Spring Security
































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