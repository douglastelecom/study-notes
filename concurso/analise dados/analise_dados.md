<div align='justify'>

## Análise de dados

>[Link](https://)
>
>30/08/2026

#### O que é dado, informação, conhecimento e inteligência?

Dado: É o fato bruto, sem contexto. Exemplo: "250", "15/04", "CG 160" etc.
Informação: Dado processado, categorizado e com contexto. Por exemplo "Pagou R$ 250,00 na semana do aluguel da moto Honda CG 160".
Conhecimneto: Detectar padrões baseados em informações. Exemplo: Locatários que pagam na segunda-feira tendem a não atrasar o pagamento.
Inteligência: Aplicar o conhecimneto para obeter uma vantagem. Por exemplo, priorizar o aluguel aos locatários que alugam as motos na segunda-feira.

#### O que é BI?

BI nada mais é que um guarda-chuva de conceitos, métodos, arquiteturas e tecnologias que visam transformar dados brutos em informações significativas. O objetivo é entregar respostas táticas e estratégicas para o negócio.

BI normalmente alimenta Sistemas de Suporte à Decisão (SSD). SSD é um ambiente frequentemente construindo em dashboards para ajudar os gestores a tomarem decisões.

#### Mapeamento e origem dos dados

Os dados não nascem prontos. Eles podem vir de qualquer lugar e é importante que sejam tratados.
Os dados podem ser dividos em dados estruturados e dados não estruturados.

**Dados estruturados:** são os dados organizados, relacionais e previsíveis. Por exemplo dados de um banco de dados relacional muito bem estruturado em classes java com o hibernate/JPA.
**Dados não estruturados:** não possuem uma estrutura predefinida ou um modelo bem claro. Por exemplo uma foto de um carro com avaria.

#### ETL, ELT, Data Watehouse e Data Lake

ETL (Extract, Transform, Load - Extrair, Transformar, Carregar): Como o próprio nome já mostra, a transformação do dado ocorre antes do seu armazenamento final. Primeiro o dado é extraído (normalmente de outros bancos relacionais), depois ele é transformado/tratado em uma staging area e só depois de transformado é que o dado é armazenado (geralmente em uma data watehouse, que também tende a ser um banco relacional).

Data Watehouse é, normalmente, um banco relacional que armazena os dados que foram tratados. Ao contrário do data lake, o dado aqui só entra depois de estar "limpo", já tratado no staging (as vezes uma api externa desenvolvida para tratar esses dados).

ELT (Extract, Load, Transform - Extrair, Carregar, Transformar): Aqui a ordem é invertida. O dado é armazenado antes (geralmente em um data lake) e só é transformado na hora da consulta.

O Data Lake é semelhate ao data watehouse, porém os dados são armazenados lá antes de serem transformados. Ele é muito utilizado no modelo ELT, e normalmente é composto por um banco de dados não relacional. Como o processamento é bem mais rápido e leve nesse tipo de banco, eles podem se dar ao luxo de tratar os dados só na hora que o usuário solicita.



</div>