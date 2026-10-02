## JPA e Hibermate

O JPA (Java Persistence API) não é um framework, mas uma especificação feita pelo javaEE. Ele define como o mapeamento e as relações dos objetos devem ser feitas em Java, mas não executa a lógica por trás.

O Hibernate é o framework que implementa a especificação JPA. Por baixo dos panos, é o Hibernate quem trabalha e conversa com o banco de dados, o JPA apenas especifica como isso é feito.

### EntityManager
É a interface principal disponibilizada pelo JPA. Ela é responsável por gerenciar as entidades, definindo persistência no banco, alteração, consultas, deletes etc.

As bancas adoram cobrar sobre o ciclo de vida das entidades que ele gerencia. Os estados da entidade são:

- Transient: Objeto foi instanciado no código com o operador new, mas não está associado ao EntityManager.
- Managed: O objeto está associado a um EntityManager ativo. Qualquer alteração em seus atributos será automaticamente sincronizada ao banco de dados após o commit ou flush.
- Detached: Objeto foi gerenciado em algum momento, possui ID e um representante no banco de dados, mas não está mais associado a nenhum EntityManager. Isso acontece quando o EntityManager foi fechado ou o objeto foi explicitamente desvinculado com um detach() ou após um clear(). Alterações feitas aqui não refletem no banco de dados.
- Removed: O objeto foi marcado para exclusão através do método .remove() do EntityManager. Ele será apagado no próximo commit.
