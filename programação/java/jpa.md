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

Os ciclos de vida existem porque o EntityManager não é um simples tradutor de SQL. Ele precisa entender o que é que foi alterado no objeto em relação a sua representação no banco de dados além de outras questões de otimização.

### Principais anotações

```java
import jakarta.persistence.*;
import org.hibernate.annotations.CreationTimestamp;
import org.hibernate.annotations.SQLDelete;
import org.hibernate.annotations.Where;
import java.time.LocalDateTime;
import java.util.ArrayList;
import java.util.List;

@Entity
@Table(name = "tb_moto")
// Anotações exclusivas do Hibernate (não são padrão JPA)
@SQLDelete(sql = "UPDATE tb_moto SET ativo = false WHERE id = ?")
@Where(clause = "ativo = true")
public class Moto {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false, unique = true, length = 8)
    private String placa;

    @Column(nullable = false)
    private String modelo;

    @Enumerated(EnumType.STRING)
    @Column(nullable = false)
    private StatusMoto status; // Enum: DISPONIVEL, ALUGADA, MANUTENCAO

    // Relacionamento Bidirecional (O lado "fraco" da relação)
    @OneToMany(mappedBy = "moto", cascade = CascadeType.ALL, fetch = FetchType.LAZY)
    private List<Locacao> locacoes = new ArrayList<>();

    // Anotação exclusiva do Hibernate
    @CreationTimestamp
    @Column(updatable = false)
    private LocalDateTime dataCadastro;

    private boolean ativo = true;

    // Construtores, Getters e Setters omitidos por brevidade
}
```

```java
import jakarta.persistence.*;
import java.time.LocalDate;

@Entity
@Table(name = "tb_locacao")
public class Locacao {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    // Relacionamento Bidirecional (O lado "forte" que tem a chave estrangeira)
    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "moto_id", nullable = false)
    private Moto moto;

    private LocalDate dataRetirada;
    private LocalDate dataDevolucao;
}
```

```java
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;
import java.util.List;

@Repository
public interface MotoRepository extends JpaRepository<Moto, Long> {
    
    // O Spring gera o SQL automaticamente: SELECT * FROM tb_moto WHERE status = ?
    List<Moto> findByStatus(StatusMoto status);
    
    // O Spring gera o SQL: SELECT * FROM tb_moto WHERE modelo LIKE %?%
    List<Moto> findByModeloContainingIgnoreCase(String modelo);
}
```

@Entity: É a única anotação obrigatória. Ela avisa o provedor de persistência que esta classe representa um registro no banco de dados. Sem ela, o código não compila num contexto de persistência.

@Table: Opcional. Serve para mudar o nome da tabela no banco (se você não usar, o JPA cria a tabela com o nome exato da classe, como Moto).

@Id e @GeneratedValue: O @Id define a chave primária. O GenerationType.IDENTITY delega a geração do ID para a coluna de auto-incremento do banco de dados (MySQL, PostgreSQL). Outra estratégia muito cobrada é a SEQUENCE, exigida por bancos mais antigos como o Oracle.

@Column: Customiza o DDL gerado (como nullable = false para obrigar o preenchimento e length para limitar o VARCHAR no banco).

@Enumerated(EnumType.STRING): Pegadinha clássica. Se você omitir isso num Enum, o JPA usa o padrão EnumType.ORDINAL, salvando no banco a posição numérica (0, 1, 2...). Se futuramente alguém mudar a ordem das palavras no Enum em Java, corrompe todo o banco de dados. O STRING salva o texto literal.

A regra do mappedBy: Em relacionamentos bidirecionais (como @OneToMany e @ManyToOne), o atributo mappedBy sempre fica na entidade que possui o @OneToMany (a Moto). Ele avisa ao JPA: "Eu não guardo a chave estrangeira aqui, quem cuida dessa coluna é o atributo 'moto' lá na classe Locacao".

O Poder do Hibernate (Implementação)
As bancas adoram testar se você sabe a diferença entre o que é JPA puro e o que é exclusividade do framework por trás dele.

@CreationTimestamp / @UpdateTimestamp: Substituem a necessidade de criar métodos interceptadores manuais (como o @PrePersist do JPA). O próprio Hibernate preenche a data do servidor automaticamente no momento do INSERT ou UPDATE.

@SQLDelete e @Where: A combinação de ouro para Soft Delete (exclusão lógica). Quando você chamar motoRepository.delete(moto), o Hibernate intercepta o comando de exclusão nativo e executa um UPDATE mudando a flag ativo para false. O @Where garante que qualquer find() ou consulta ignore registros onde ativo = false, tudo de forma transparente.

Os Tipos de Cascade (Foco das Bancas)
As opções derivam do enumerador CascadeType e refletem diretamente as mudanças de estado do EntityManager:

- CascadeType.PERSIST: O "inserir". Quando a entidade pai transita de Transient para Managed, todos os filhos vinculados a ela também recebem um INSERT no banco.

- CascadeType.MERGE: O "atualizar". Se você ressincronizar o pai (que estava Detached) usando o merge, o JPA varre a lista de filhos e dispara o UPDATE neles também.

- CascadeType.REMOVE: O "deletar". Se a entidade pai for removida do banco, todas as entidades filhas associadas também sofrem um DELETE.

- CascadeType.ALL: Agrupa todas as operações acima (além de REFRESH e DETACH). É a escolha padrão para relacionamentos de composição forte, onde o filho não faz o menor sentido de existir sem o pai.

Cuidado para não confundir com o oprhanRemoval. A função do orphanRemoval = true: Ele é um atributo exclusivo das anotações @OneToMany e @OneToOne que cobre exatamente essa falha. Se você quebrar a relação deum filho com o pai (quebrando o vínculo em memória), o JPA intercepta isso e emite um DELETE imediato no banco de dados para aquele registro específico, mesmo que a moto continue existindo perfeitamente.
