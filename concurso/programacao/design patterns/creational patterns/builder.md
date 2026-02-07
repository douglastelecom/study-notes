<div align='justify'>

## BUILDER

>[Link](https://refactoring.guru/design-patterns/builder)
>
>11/11

#### PROBLEMA

Sua classe possui diversos parâmetros que devem ser definidos na sua instânciação, porém nem todos esses parâmetros são obrigatórios. Você pode então criar diversos construtores respeitando a não obrigatoriedade de alguns parâmetros, ou então definir um construtor imenso que irá abrigar todos os parâmetros (e caberá ao cliente definir como null os parâmetros não obrigatórios que ele não quiser utilizar).

O problema é que tanto a solução de diversos construtores quanto a solução de um construtor imenso não são elegantes e são muito trabalhosas para o cliente.

#### SOLUÇÃO

O builder permite que o usuário crie classes apenas coms os atributos do seu interesse. Uma classe estática builder é criada dentro da classe desejada (nesse exemplo, `Usuario`).

#### IMPLEMENTAÇÃO DO CLIENTE

##### ANTES

```JAVA
Usuario usuario = new Usuario("Douglas", "douglas@email.com", 30, "99999-9999", "Rua X", true);
```

##### DEPOIS

```java
Usuario usuario = new Usuario.Builder()
        .nome("Douglas")
        .email("douglas@email.com")
        .idade(30)
        .telefone("99999-9999")
        .ativo(true)
        .build();
```

#### CLASSES

```JAVA
public class Usuario {
    private String nome;
    private String email;
    private int idade;
    private String telefone;
    private String endereco;
    private boolean ativo;

    private Usuario(Builder builder) {
        this.nome = builder.nome;
        this.email = builder.email;
        this.idade = builder.idade;
        this.telefone = builder.telefone;
        this.endereco = builder.endereco;
        this.ativo = builder.ativo;
    }

    public static class Builder {
        private String nome;
        private String email;
        private int idade;
        private String telefone;
        private String endereco;
        private boolean ativo;

        public Builder nome(String nome) {
            this.nome = nome;
            return this;
        }

        public Builder email(String email) {
            this.email = email;
            return this;
        }

        public Builder idade(int idade) {
            this.idade = idade;
            return this;
        }

        public Builder telefone(String telefone) {
            this.telefone = telefone;
            return this;
        }

        public Builder endereco(String endereco) {
            this.endereco = endereco;
            return this;
        }

        public Builder ativo(boolean ativo) {
            this.ativo = ativo;
            return this;
        }

        public Usuario build() {
            return new Usuario(this);
        }
    }
}
```


</div>