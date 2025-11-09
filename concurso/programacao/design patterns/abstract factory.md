<div align='justify'>

## ABSTRACT FACTORY

>[Link](https://refactoring.guru/pt-br/design-patterns/java)
>
>09/11

#### PROBLEMA

E se ao invés de apenas renderizar um dialog a biblioteca também permitisse tocar uma música? Dessa forma, seria necessário garantir que o dialog e a música seriam criados para o mesmo SO.

#### Solução

O abstract factory é uma fábrica de fábricas. Ao invés de criar uma fábrica de dialogs `DialogFactory`, cria-se um `FactoryProvider` que irá retornar uma factory (`WindowsFactory` ou `LinuxFactory`) que implementa a interface ``Factory``.

Dessa forma, sempre que um usuário quiser um dialog ou tocar uma música, ele terá o factory correto para o seu SO.

##### Exemplo de Instânciação

```JAVA
Factory factory = ProviderFactory.getFactory();

Dialog dialog = factory.createDialog();
dialog.render("Olá, mundo!");

Music music = factory.createMusic();
music.play('teste.wav')
```

##### Interfaces

```JAVA
public interface Factory {
    Dialog createDialog();
    Music createMusic();
}
```

```JAVA
public interface Dialog {
    void render(String message);
}
```

```JAVA
public interface Music {
    void play(String fileName);
}
```

##### Produtos concretos

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

```JAVA
public class WindowsMusic implements Music {
    @override
    public void play(String filename){
      /**
         * código que toca música no windows
      */  
    }
}
```

```JAVA
public class LinuxMusic implements Music {
    @override
    public void play(String filename){
      /**
         * código que toca música no linux
      */  
    }
}
```

##### Factories

```JAVA
public class WindowsFactory implements Factory{

    public Dialog createDialog(){
        return new WindowsDialog();
    }

    public Music createMusic(){
        return new WindowsMusic();
    }
}
```

```JAVA
public class LinuxFactory implements Factory{

    public Dialog createDialog(){
        return new LinuxDialog();
    }

    public Music createMusic(){
        return new LinuxMusic();
    }
}
```

##### Provider
```JAVA
public class FactoryProvider {

    public static Factory getFactory() {
        String osName = System.getProperty("os.name").toLowerCase();

        if (osName.contains("win")) {
            return new WindowsFactory();
        } else {
            return new LinuxFactory();
        }
    }
}
```


</div>