<div align='justify'>

## Análise de dados

>[Link](https://)
>
>30/08/2026

### O que é dado, informação, conhecimento e inteligência?

Dado: É o fato bruto, sem contexto. Exemplo: "250", "15/04", "CG 160" etc.
Informação: Dado processado, categorizado e com contexto. Por exemplo "Pagou R$ 250,00 na semana do aluguel da moto Honda CG 160".
Conhecimneto: Detectar padrões baseados em informações. Exemplo: Locatários que pagam na segunda-feira tendem a não atrasar o pagamento.
Inteligência: Aplicar o conhecimneto para obeter uma vantagem. Por exemplo, priorizar o aluguel aos locatários que alugam as motos na segunda-feira.

### O que é BI?

BI nada mais é que um guarda-chuva de conceitos, métodos, arquiteturas e tecnologias que visam transformar dados brutos em informações significativas. O objetivo é entregar respostas táticas e estratégicas para o negócio.

BI normalmente alimenta Sistemas de Suporte à Decisão (SSD). SSD é um ambiente frequentemente construindo em dashboards para ajudar os gestores a tomarem decisões.

### Mapeamento e origem dos dados

Os dados não nascem prontos. Eles podem vir de qualquer lugar e é importante que sejam tratados.
Os dados podem ser dividos em dados estruturados e dados não estruturados.

**Dados estruturados:** são os dados organizados, relacionais e previsíveis. Por exemplo dados de um banco de dados relacional muito bem estruturado em classes java com o hibernate/JPA.
**Dados não estruturados:** não possuem uma estrutura predefinida ou um modelo bem claro. Por exemplo uma foto de um carro com avaria.

### ETL, ELT, Data warehouse e Data Lake

ETL (Extract, Transform, Load - Extrair, Transformar, Carregar): Como o próprio nome já mostra, a transformação do dado ocorre antes do seu armazenamento final. Primeiro o dado é extraído (normalmente de outros bancos relacionais), depois ele é transformado/tratado em uma staging area e só depois de transformado é que o dado é armazenado (geralmente em uma data warehouse, que também tende a ser um banco relacional).

Data warehouse é, normalmente, um banco relacional que armazena os dados que foram tratados. Ao contrário do data lake, o dado aqui só entra depois de estar "limpo", já tratado no staging (as vezes uma api externa desenvolvida para tratar esses dados).

ELT (Extract, Load, Transform - Extrair, Carregar, Transformar): Aqui a ordem é invertida. O dado é armazenado antes (geralmente em um data lake) e só é transformado na hora da consulta.

O Data Lake é semelhate ao data warehouse, porém os dados são armazenados lá antes de serem transformados. Ele é muito utilizado no modelo ELT, e normalmente é composto por um banco de dados não relacional. Como o processamento é bem mais rápido e leve nesse tipo de banco, eles podem se dar ao luxo de tratar os dados só na hora que o usuário solicita.

### Modelagem dimensional

A modelagem dimensional é o padrão arquitetural dos bancos de dados de leitura analítica e data warehouse. A ideia é voltar o nível de normalização que é feita nos bancos relacionais, ao invés de haver várias tabelas que se relacionam, haverá apenas uma (ou poucas outras) tabelas grandes, chamadas de tabelas dimensão, que são uma junção das tabelas menores. Isso naturalmente aumenta a repetição dos dados, porém ter uma só tabela grande (ou poucas mais) diminui drasticamente o tempo de processamento.

Tabelas fato: tabelas normais presentes em bancos de dado relacional.
Tabelas dimensão: junção de tabelas fato em uma tabela maior.

### OLTP x OLAP

O OLTP (Online Transactional Processing) é o banco de dados relacional padrão. Ele é otimizado para transações rápidas e pontuais (insert, update etc). 

O OLAP (Online Analytical Processing) é um motor analítico otimizado para consultas pesadas (select). Consegue processar milhares de registros de uma só vez para gerar relatórios gerenciais sem impactar o sistema. Ele utiliza as tabelas dimensão (modelagem dimensional) e as transforma em estruturas de cubos onde uma das dimensões do cubo é o tempo. Dessa forma, os dados já foram cruzados em relação ao tempo, o que facilita na hora da consulta porque o processamento já foi realizado.

O cubo nada mais é que uma estrutura que armazena o resultado dos dados já previamente calculados em relação ao tempo. Para navegar por esse cubo no Power BI ou outra ferramenta visual, você utiliza as Operações OLAP:

- Drill-down (Aprofundar): É descer no nível de detalhe. Você está vendo o faturamento de "2026". Dá um duplo clique e a visão quebra para "Semestres", depois "Meses", até chegar em "Dias".

- Roll-up (Resumir): É o exato oposto do drill-down. Você sobe o nível de detalhe, saindo do faturamento diário para o faturamento anual consolidado.

- Slice (Fatiar): Você corta uma "fatia" do cubo fixando apenas uma dimensão. Exemplo: ignorar todo o resto e fatiar o cubo para ver apenas os dados onde o Pagamento = "Pix".

- Dice (Em Cubos menores): Você fixa duas ou mais dimensões ao mesmo tempo, extraindo um sub-cubo. Exemplo: analisar apenas os dados onde Pagamento = "Pix" E Moto = "CG 160".

- Pivot (Rotacionar): Você inverte as linhas e colunas no painel visual para ver os dados de um ângulo diferente (exatamente como funciona uma Tabela Dinâmica no Excel).

### Mineração de dados

A mineração de dados busca padrões ocultos, correlações invisíveis e anomalias.

Técnica de associação: Descobre eventos que ocorrem juntos. Exemplo: Sempre quem compra leite também compra fralda.

Técnicas de agrupamento (clustering): Algorítmo que agrupa dados por semelhança. Você não precisa definir as classes previamente, ele irá agrupar dados que julga parecidos e caberá a você estabelecer as categorias.

Técnicas de classificação: Você define as categorias, as regras e o algoritmo irá classificar os dados em grupos.

### Machine Learning

Enquanto a mineração foca em descobrir padrões ocultos, o machine learning utiliza esses padrões para construir modelos preditivos tentando prever o futuro.

Aprendizado supervisionado: O algoritmo é treinado com um histórico de dados e uma resposta conhecida.

Técnicas de classificação: A ideia é que o modelo tente classificar os dados que são enviados a ele a partir dos padrões que já foram analisados.

Técnicas de Regressão: Utilizado para tentar prever um valor contínuo e numérico. O algorítmo tenta prever "o quanto", não apenas "sim" ou "não".

</div>