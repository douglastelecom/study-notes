<div align='justify'>

## TÍTULO 1

>Arquivos da valecard
>
>23 de Janeiro de 2025

# Frameworks e Tecnologias da ValKard

## Arquiteturas de Design

### **ADR-001**

**Problema:** Como desenvolver sistemas corporativos que suportem diferentes tipos de clientes, como navegadores de desktop, navegadores móveis e aplicativos móveis nativos? Além disso, como expor esses aplicativos (APIs) para terceiros?  
**Solução:** Arquitetura de microsserviços.  

---

### **ADR-002**

**Problema:** Como encapsular em um único ponto de entrada as chamadas aos ativos de negócios corporativos?  
**Solução:** Serviço de Gateway API. Garante segurança, controle de acesso, limites de solicitações, parceria e monetização.  

---

### **ADR-003**

**Problema:** Como administrar os aplicativos de lado servidor de modo a promover uma solução gerenciável, de baixo acoplamento, baixo impacto na implantação, alta disponibilidade, elasticidade e resiliência?  
**Solução:** Paradigma de malha de serviços (Service Mesh). Permite telemetria, balanceamento baseado em tráfego de informações.  

---

## **Assunto: O que é Service Mesh?**

Camada de infraestrutura dedicada para gerenciar a comunicação entre microsserviços em um sistema distribuído. Atua como um intermediário entre os serviços, fornecendo funcionalidades como:  

- Roteamento de tráfego  
- Balanceamento de carga  
- Segurança  
- Observabilidade  
- Resiliência  
- Gestão de configuração  

---

### **ADR-004 – Database per Service**

**Problema:** Como reduzir a dependência de inúmeros sistemas de um único banco de dados monolítico?  
**Solução:** Utilizar o padrão de 1 BD por serviço.  

---

### **ADR-005: Organizar as integrações de negócio em containers**

**Problema:** Como permitir que diferentes sistemas de diferentes plataformas se comuniquem de forma eficaz?  
**Solução:** Implantação de uma camada de integração capaz de prover conectores para diferentes tipos de protocolos.  

---

### **ADR-006 – Distribuir alterações via serviço de streaming**

**Problema:** Como criar uma plataforma unificada, de alta capacidade e baixa latência para tratamento de dados em tempo real, maciçamente escalável e que permita conectar facilmente com diversas fontes de dados?  
**Solução:** Adotar um serviço de streaming.  

---

### **ADR-007 – Organizar as funções de negócio através de serviços em nuvem**

**Problema:** Como prover uma solução de microsserviços que atenda alto volume transacional a um custo gerenciável?  
**Solução:** Adotar serviços de nuvem: baixo custo, boa performance, resiliência e observância.  

---

### **ADR-008 – Realizar a observância analítica e de logs**

**Problema:** Como monitorar e identificar gaps e pontos de melhoria em seu ambiente de tecnologia através de logs?  
**Solução:** Observância analítica e centralizada de logs.  

---

### **ADR-009 – Implementar as telas dos sistemas utilizando Single Page Applications**

**Problema:** Qual tecnologia para ser utilizada em aplicações web?  
**Solução:** Adoção de Single Page Applications, prática atual e de mercado. Permite telas responsivas, dinâmicas e com maior performance.  

---

### **ADR-011 – Implementação de teste unitário front-end e de integração backend**

**Problema:** Como garantir a qualidade da aplicação frontend desenvolvida em Angular?
**Solução:** Para endereçar problema, iremos adotar os testes unitários e teste de integração com o coverage de 85% do projeto, garantindo a qualidade da aplicação frontend.

---


</div>