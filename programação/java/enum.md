<div align='justify'>

## ENUM

>[Link](https://)
>
>15/02

A enum é muito parecido com uma classe normal do java. A diferença é que ela armazena internamente instâncias `static final` dela mesma com uma nomeclatura mais simplifiacda.

Por exemplo, no exemplo abaixo da enum, ao invés de ser necessário escrever:

```java
public static final NivelAcessoEnum ADM = new NivelAcessoEnum(1, "Administrador");
public static final NivelAcessoEnum EDITOR = new NivelAcessoEnum(2, "Editor de Conteúdo");
public static final NivelAcessoEnum VISITANTE = new NivelAcessoEnum(3, "Apenas Leitura");
```

O padrão definido para o enum foi:

```java
ADM(1, "Administrador"), 
EDITOR(2, "Editor de Conteúdo"), 
VISITANTE(3, "Apenas Leitura");
```

E elas SEMPRE devem vir primeiro.

Abaixo o exemplo de um código completo de enum.

```java
public enum NivelAcessoEnum {
    // 1. As instâncias (devem vir primeiro)
    // Pense nelas como: public static final NivelAcessoEnum ADM = new NivelAcessoEnum(1, "Administrador");
    ADM(1, "Administrador"), 
    EDITOR(2, "Editor de Conteúdo"), 
    VISITANTE(3, "Apenas Leitura");

    // 2. Os atributos (o que cada item "guarda")
    private final int codigo;
    private final String descricao;

    // 3. O Construtor (como cada item é montado)
    // O Java não deixa você usar "public" aqui. Ele é privado por padrão.
    NivelAcesso(int codigo, String descricao) {
        this.codigo = codigo;
        this.descricao = descricao;
    }

    // 4. Métodos (o que o enum sabe fazer)
    public int getCodigo() {
        return codigo;
    }

    public String getDescricao() {
        return descricao;
    }
}
```

Exemplo chamando a enum:

```java
public class TesteEnum {
    public static void main(String[] args) {
        NivelAcesso userNivel = NivelAcesso.ADM;

        System.out.println("Seu cargo é: " + userNivel.getDescricao());
        System.out.println("Código interno: " + userNivel.getCodigo());
        
        // Você pode comparar diretamente com == (é seguro e performático)
        if (userNivel == NivelAcesso.ADM) {
            System.out.println("Acesso total liberado!");
        }
    }
}
```

</div>