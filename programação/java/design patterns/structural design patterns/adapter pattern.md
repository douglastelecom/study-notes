<div align='justify'>

## Adapter Pattern

>[Link](Claude)
>
>02/07/2026

O adaptador ele serve para adaptar uma saída para uma entrada, de forma que os valores e os tipos sejam compatíveis.
Imagina que eu preciso usar um método de uma classe (api legado) `PagamentoExternoLegado` do tipo `void efetuarCobranca(String valor)`. No entanto, meu sistema está todo acoplado para trabalhar com o método `void pagar(double valor)` (perceba que os tipos e o nome são diferentes).
Ao invés de chamar diretamente o método `efetuarCobranca(String valor)`, eu vou chamar o método pagar() de uma classe de adaptação que irá implementar a interface `Pagamento`.

Meu código só vai conhecer a interface pagamento. Como esse pagamento acontece não o interessa. Dessa forma eu posso simplesmente usar outra API se eu desejar e substituí-la no adaptador e meu código ficará inalterado.

#### Exemplo

```java
//Interface
public interface Pagamento {
    void pagar(double valor);
}
```


```java
//Método de uma API legada que não pode ser alterada
public class PagamentoExternoLegado {
    public void efetuarCobranca(String valorEmCentavos) {
        System.out.println("Cobrança de " + valorEmCentavos + " centavos processada via sistema legado.");
    }
}
```

```java
//Classe adaptadora
public class AdapterPagamentoLegado implements Pagamento {

    private PagamentoExternoLegado pagamentoLegado;

    public AdapterPagamentoLegado(PagamentoExternoLegado pagamentoLegado) {
        this.pagamentoLegado = pagamentoLegado;
    }

    @Override
    public void pagar(double valor) {
        // Aqui acontece a "tradução"
        String valorEmCentavos = String.valueOf((int) (valor * 100));
        pagamentoLegado.efetuarCobranca(valorEmCentavos);
    }
}
```

```java
//Usabilidade
public class Main {
    public static void main(String[] args) {
        Pagamento pagamento = new AdapterPagamentoLegado(new PagamentoExternoLegado());
        pagamento.pagar(150.90); // seu código só conhece a interface Pagamento
    }
}
```
</div>