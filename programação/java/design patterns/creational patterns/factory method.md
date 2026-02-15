<div align='justify'>

## FACTORY METHOD

>[Link](https://refactoring.guru/pt-br/design-patterns/java)
>
>09/11

#### PROBLEMA

##### Problema 1

Imagine uma biblioteca Java que abre janelas (dialogs) com mensagens no Windows. Porém você precisa exetender essa biblioteca para funcionar em Linux também, no entanto todo o seu código já está acoplado ao windows, e para que a biblioteca funciona também em linux seria necessário reajustar todo o código.

##### Problema 2

Imagine que o seu software permite renderizar o dialog em diversos sistemas operacionais e que não é do interesse do cliente da bilioteca saber quais classes existem para cada sistema operacional. Ele só precisa saber que o dialog pertence à classe `Dialog` e que possui um método `render()`.

#### Solução

O padrão factory method recomenda criar uma superclasse (ou interface), por exemplo `Dialog`, e não instanciar os dialogs diretamente, como `new DialogWindows()` ou `new DialogLinux()`. Ao invés de instanciar as classes diretamente, haverá uma classe `DialogFactory` responsável por retornar o dialog certo para você.

##### Exemplo de Instânciação

```JAVA
Dialog dialog = DialogFactory.createDialog();
dialog.render("Olá, mundo!");
```

##### Interface Dialog:

```JAVA
public interface Dialog {
    void render(String message);
}
```

##### Produtos Concretos

```JAVA
public class WindowsDialog implements Dialog {
    @override
    public void render(String message){
      /**
         * código que renderiza um dialog no windows
      */  
    }
}
```

```JAVA
public class LinuxDialog implements Dialog {
    @override
    public void render(String message){
      /**
         * código que renderiza um dialog no linux
      */  
    }
}
```

##### Factory

```JAVA
public class DialogFactory {

    public Dialog createDialog(){
        if (System.getProperty("os.name").equals("Windows 10")) {
            return new WindowsDialog();
        } else {
                return new LinuxDialog();
          }
    }
}
```


</div>