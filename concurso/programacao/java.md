<div align='justify'>

## JAVA

>[Link](https://)
>
>08 Outubro de 2024

#### Servlets

Um servlet no java é um componente de software que lida com requisições HTTP de uma aplicação WEB. A interface mais comumente utilizada é a ``javax.servlet.Servlet`` que define os métodos que os servlets devem implementar, permitindo que processem e gerem respostas as requisições http. Os métodos são ``init()``, utilizado para instanciar um servlet, o ``service()`` para processar a requisição http e o ``destroy()`` quando um servlet não for mais utilizado.

No Spring Boot, os servlets são "substituídos" por controllers, porém existe um servlet central denominado ``DispatcherServlet`` que é responsável por receber todas as requests HTTPS e encaminhá-las ao seu devido controller. A diferença entre um servlet padrão e um controller do spring boot é que o controller possui uma abordagem mais abstrata e simplificada, podendo ser considerado de "mais alto nível".

#### DIFERENÇA ENTRE JAVAX, JAVA EE E JAKARTA EE

Javax é um prefixo utilizado por várias APIs que as definem como sendo parte das extensões padrões do JAVA. Resumindo, é um pacote que contém os principais pacotes e APIs da linguagem java.

Java EE foi uma plataforma para desenvolvimento de aplicações corporativas Java até 2017. É uma evolução do Java SE (Standard Edition) e foi projetada para a desenvolvimento de grandes sistemas corporativos e distribuídos, oferecendo um conjunto de especificações e APIs que facilitam a construção de aplicações robustas e seguras. Dentre suas principais contribuições estão: EJB, JPA, JAX-RS, JAX-WS, Servlets e JSP e JSF. É importante observar que boa parte das bibliotecas e APIs fornecidas pela Java EE começa com o prefixo Javax, pois são extensões padrões do Java.

O Jakarta EE é a continuação do projeto Java EE, que foi doado pela Oracle para a Eclipse Foundation. A mudança de nome ocorreu devido a restrições de marca registrada com o uso do nome "Java".

#### DIFERENÇA ENTRE JSP E JSF

O JSP é uma tecnologia simples voltada para a renderização dinâmica de HTML através de tags especiais como ``<% %>``. A extensão dos arquivos html é jsp, como "index.jsp".

O JSF, ao contrário do JSP que é basicamente uma camada de exibição, é um framework completo que abstrai a criação de interfaces web e facilita a construção de componentes reutilizáveis (botões, tabelas, formulários) etc. Segue um padrão de component-based development (desenvolvimento baseado em componentes) e facilita a separação entre a lógica de apresentação e a lógica de negócios.

JSF é orientado a componentes, ou seja, ele permite que você crie interfaces utilizando componentes prontos, como campos de entrada, formulários e tabelas, que podem ser gerenciados pelo ciclo de vida do JSF. Utiliza páginas XHTML.
</div>