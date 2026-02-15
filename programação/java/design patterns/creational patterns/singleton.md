<div align='justify'>

## SINGLETON

>[Link](https://www.digitalocean.com/community/tutorials/java-singleton-design-pattern-best-practices-examples)
>
>07/02/2026

#### PROBLEMA

E se eu quiser garantir que haja apenas uma instância da minha classe no sistema?

#### Solução

O padrão singleton garante isso. O singleton pode ser implementado com diferentes abordagens, mas todas elas seguem três princípios:

1. Construtor sempre privado.
2. Uma variável `static` na mesma classe para salvar a instância.
3. Um método `static` que retorne essa variável.

#### ABORDAGEM 1: EAGER INITIALIZATION

Assim que o sistema sobe, uma instância da classe é criada e salva na variável estática. É uma boa abordagem para classes simples e pequenas, mas para classes mais pesadas, como drivers, file systens etc é melhor evitar para não sobrecarregar desnecessariamente o sistema (evitar que a classe seja instanciada sem ser utilizada).

```java
package com.journaldev.singleton;

public class EagerInitializedSingleton {

    private static final EagerInitializedSingleton instance = new EagerInitializedSingleton();

    // private constructor to avoid client applications using the constructor
    private EagerInitializedSingleton(){}

    public static EagerInitializedSingleton getInstance() {
        return instance;
    }
}
```

#### ABORDAGEM 2: STATIC BLOCK INITIALIZATION

É muito parecido com a abordagem anterior de inicialização eager, a diferença é que agora a variável é instanciada dentro de um block "tratado" como uma runtimeException. Tanto a static block e a eager initialization criam uma instância da classe antes mesmo de ser utilizada.

```java
package com.journaldev.singleton;

public class StaticBlockSingleton {

    private static StaticBlockSingleton instance;

    private StaticBlockSingleton(){}

    // static block initialization for exception handling
    static {
        try {
            instance = new StaticBlockSingleton();
        } catch (Exception e) {
            throw new RuntimeException("Exception occurred in creating singleton instance");
        }
    }

    public static StaticBlockSingleton getInstance() {
        return instance;
    }
}
```

#### ABORDAGEM 3: LAZY INITIALIZATION

Aqui a instância só é criada quando o método `getInstance()` é chamado. Perceba que a instância só é criada dentro do método, ao contrário das abordagens anteriores onde a instância era criada fora de um método.
Observação: a variável instance ainda precisa ser static, porque métodos statics só podem trabalhar com variáveis do tipo static.

```java
package com.journaldev.singleton;

public class LazyInitializedSingleton {

    private static LazyInitializedSingleton instance;

    private LazyInitializedSingleton(){}

    public static LazyInitializedSingleton getInstance() {
        if (instance == null) {
            instance = new LazyInitializedSingleton();
        }
        return instance;
    }
}
```

#### ABORDAGEM 4: THREAD SAFE SINGLETON

Para garantir que apenas uma thread irá gerar a instância é recomendado o uso do synchronized.

```java
package com.journaldev.singleton;

public class ThreadSafeSingleton {

    private static ThreadSafeSingleton instance;

    private ThreadSafeSingleton(){}

    public static synchronized ThreadSafeSingleton getInstance() {
        if (instance == null) {
            instance = new ThreadSafeSingleton();
        }
        return instance;
    }

}
```

Para reduzir o overhead do synchronized (ele reduz a performance do sistema), podemos inserir o synchronized dentro do if.

```java
public static ThreadSafeSingleton getInstanceUsingDoubleLocking() {
    if (instance == null) {
        synchronized (ThreadSafeSingleton.class) {
            if (instance == null) {
                instance = new ThreadSafeSingleton();
            }
        }
    }
    return instance;
}
```

#### ABORDAGEM 5: BILL PUGH SINGLETON IMPLEMENTATION

Essa é a forma mais elegante e comum para se utilizar singleton. O java define que uma classe só é carregada na memória quando ela é de fato utilizada ao menos UMA VEZ, então a classe interna `SingletonHelper` só será carregada e consquentemente criará a instância `new BillPughSingleton()` na exata primeira vez que for chamada.

A beleza dessa abordagem é que ela transfere a responsabilidade para a própria java virtual machine (JVM). Como o processo de inicialização de uma classe em Java é inerentemente thread-safe, não é necessário sequer utilizar synchronized. O ` static final` também ajuda a garantir que a variável não será alterada e que existirá apenas uma.

```java
package com.journaldev.singleton;

public class BillPughSingleton {

    private BillPughSingleton(){}

    private static class SingletonHelper {
        private static final BillPughSingleton INSTANCE = new BillPughSingleton();
    }

    public static BillPughSingleton getInstance() {
        return SingletonHelper.INSTANCE;
    }
}
```

#### ABORDAGEM 6: ENUM SINGLETON

Como o valor de um enum é instanciado apenas uma vez, também é possível utilizar essa abordagem para garantir que uma classe seja singleton. A grande vantagem do enum é que ele é a abordagem mais segura, pois o java trata serialization e reflection de enums de forma especial.
A desvantagem é que os enums são inflexíveis, por exemplo, não permitem lazy initialization.

```java
package com.journaldev.singleton;

public enum EnumSingleton {

    INSTANCE;

    public static void doSomething() {
        // do something
    }
}
```


</div>