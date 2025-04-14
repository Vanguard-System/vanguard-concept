# **Vanguard - Sistema de Gerenciamento para Empresa de Turismo**

## 📌 Capa
**Título do Projeto:** Sistema de Gerenciamento de Viagens para Empresa de Turismo  
**Nome do Estudante:** Lucas Willian de Souza Serpa  
**Curso:** Engenharia de Software  
**Data de Entrega:**  

---

## 📌 Resumo
Este documento apresenta a especificação de um sistema de gerenciamento de viagens para uma empresa de turismo. O sistema permitirá a **criação de orçamentos, gerenciamento de viagens, controle financeiro e cálculo de salários de motoristas**.  

O fluxo do sistema será o seguinte:  
1. O **usuário fará login** no sistema.  
2. Criará um **orçamento de viagem**, que poderá ser **exportado em PDF** para envio ao cliente.  
3. O orçamento ficará **em aguardo** até o cliente aceitar.  
4. Se aceito, a **viagem será confirmada**, e o **motorista será notificado via email**.  
5. O sistema manterá um **histórico de viagens**, listando as **viagens ocorridas e futuras**.  
6. Após a viagem, o sistema permitirá o **cálculo do salário do motorista**, considerando os dias trabalhados e variáveis adicionais.  

O projeto será desenvolvido com **React** no front-end, **NestJS** no back-end e utilizará **MySQL** como banco de dados, com suporte a notificações via **email** para motoristas.  

---

## 📌 Introdução

### **Contexto**
Empresas de turismo precisam gerenciar motoristas, ônibus e viagens de maneira eficiente para garantir organização e controle financeiro. Atualmente, a administração dessas informações pode ser complexa e suscetível a erros manuais.  

### **Justificativa**
A criação deste sistema busca otimizar o gerenciamento da empresa de turismo do usuário, proporcionando um ambiente centralizado para **controle de orçamentos, viagens, custos operacionais e pagamento de motoristas**. Isso reduzirá o trabalho manual e melhorará a precisão dos cálculos financeiros.  

---

## 📌 Processo da Venda e da Viagem

### **Origem da Venda**
Os clientes costumam entrar em contato com a empresa de três formas:  
1. **Contato direto** do cliente com a empresa.  
2. **Indicação** por empresas parceiras.  
3. **Prospecção ativa** feita pelo setor comercial da empresa.  

### **Como é feito o orçamento?**
O orçamento é calculado com base nos seguintes critérios:  

1️⃣ **Definição da Quilometragem**  
   - É considerada a **ida e a volta** da viagem.  
   - É adicionado um **extra de 7%** para deslocamentos dentro da cidade de destino.  

2️⃣ **Cálculo do Valor da Viagem**  
   - Multiplicação da quilometragem total por **R$ 8,00/km** (este valor é variável e pode ser alterado no sistema).  

3️⃣ **Cálculo de Impostos**  
   - Adição de **8,33%** sobre o valor da viagem para cobrir impostos (também configurável).  

4️⃣ **Custos Adicionais**  
   - **Pedágios:** São adicionados caso existam na rota.  
   - **Pagamento do motorista:** R$ **200 por dia** (variável, dependendo da duração da viagem).  

5️⃣ **Cálculo Final**  
   - Após considerar todos os custos, o orçamento final é gerado e enviado ao cliente.  

### **Relacionamento com o Cliente**

- O cliente geralmente realiza o pagamento **dois dias antes** da viagem.  
- Em casos de **viagens de última hora**, o pagamento ocorre no momento do envio da lista de passageiros.  
- Sempre que possível, o cliente recebe o **ônibus maior**, mas se ele não estiver disponível, será utilizado o menor (sem alteração no preço).  

---

## 📌 Cálculo de Validação do Orçamento

Após gerar o orçamento, um **cálculo de validação** é feito para garantir que o preço cobrado está adequado.  

1️⃣ **Cálculo do Consumo de Diesel**  
   - Considera que **o ônibus faz 3 km por litro**.  
   - O cálculo é:  
     ```
     Quilometragem total ÷ 3 = Litros consumidos
     ```  

2️⃣ **Cálculo do Custo do Diesel**  
   - Multiplicação do consumo de litros pelo valor do diesel (**R$ 7,00 por litro**).  

3️⃣ **Validação do Orçamento**  
   - O custo total do diesel é dividido pelo valor total da viagem:  
     ```
     (Custo do diesel ÷ Valor total da viagem) × 100 = Percentual de custo
     ```  
   - Se este valor for **superior a 30%**, significa que a viagem foi subcotada.  
   - Para corrigir, o sistema **ajusta automaticamente** o valor de R$ 8,00/km (definido na etapa de orçamento).  

---

## 📌 Viagem Finalizada e Cálculo do Salário do Motorista

Após a conclusão da viagem, o sistema calculará o pagamento do motorista considerando:  

✅ **R$ 200 por dia** trabalhado.  
✅ **R$ 35 por dia de Vale-Refeição (VR)**.  
✅ **R$ 50 extra** caso o motorista tenha **limpado o ônibus antes da viagem**.  
✅ **R$ 35 adicionais** para **lavagem das capas dos bancos** (caso necessário).  

O pagamento do motorista é sempre realizado **após a viagem ser concluída**.  

---

## 📌 Custos Previstos e Não Previstos

### **Custos Não Previstos**
- **Quebra do veículo:**  
  - Se o ônibus apresentar problemas mecânicos, o motorista tentará resolver.  
  - Caso não consiga, um mecânico será acionado, e **a empresa cobre os custos**.  
  - Se o veículo não for consertado a tempo, um **ônibus reserva** ou uma **empresa parceira** realizará o transporte.  

### **Custos Previstos**
- **Manutenção periódica:**  
  - A cada **35 mil km** os ônibus passam por uma **revisão completa**.  

---

## 📌 Especificação Técnica

### **Requisitos Funcionais (RF)**

- Verificar todos os requisitos no wiki com o link abaixo:
  
https://github.com/Lucaswillians/vanguard-concept/wiki/Especifica%C3%A7%C3%A3o-T%C3%A9cnica-%E2%80%90-Requisitos-de-Software  

---

## 📌 Módulo de Cálculo de Salários dos Motoristas

### 🔹 **Métodos de Pagamento Suportados**
1️⃣ **Salário Fixo + Adicionais por Viagem**  
   - O motorista recebe um valor fixo mensal.  
   - Pode haver bônus por viagem realizada.  

2️⃣ **Pagamento por Viagem**  
   - O motorista recebe um valor fixo por quilômetro rodado ou por viagem concluída.  

3️⃣ **Comissão sobre o Valor da Viagem**  
   - O motorista recebe uma porcentagem do valor total da viagem.  

### 🔹 **Funcionalidades do Módulo**
✅ Cadastro de motoristas com tipo de pagamento.  
✅ Cálculo automático de salários com base nas viagens realizadas.  
✅ Geração de relatório mensal de pagamento.  
✅ Histórico de pagamentos anteriores.  
✅ Exportação do salário em **PDF** (como um "holerite").  

---

## 📌 Considerações de Design

### **Visão Inicial da Arquitetura**
A aplicação seguirá uma arquitetura baseada em três camadas principais:

- **Frontend (React)**: Interface para o administrador realizar o gerenciamento das viagens e motoristas.  
- **Backend (NestJS)**: Lógica de negócios e comunicação com o banco de dados.  
- **Banco de Dados (MySQL)**: Armazena todas as informações do sistema.  

### **Padrões de Arquitetura**
- **MVC (Model-View-Controller)**: Separação entre interface, lógica de negócio e persistência de dados.  
- **Modelos C4**: Para representação da arquitetura.  

---

## 📌 Stack Tecnológica

### **Linguagens de Programação**
- **Frontend**: JavaScript/TypeScript com React.  
- **Backend**: TypeScript com NestJS.  
- **Banco de Dados**: SQL com MySQL.  

### **Frameworks e Bibliotecas**
- React (UI)  
- NestJS (API)  
- Axios (requisições HTTP para buscar preço do combustível)  
- TypeORM (gerenciamento do banco de dados)  

### **Ferramentas de Desenvolvimento e Gestão**
- Docker (contêineres)  
- GitHub (controle de versão)  
- GitHub Actions (gestão do projeto)  

---

## 📌 Próximos Passos

- Desenvolvimento do **MVP** com as principais funcionalidades.  
- Testes internos para validação do sistema.  
- Implementação do módulo de **cálculo de salários** dos motoristas.  
- Revisão final e ajustes conforme feedback do usuário.  

---

## 📌 Referências
- Documentação oficial do React e NestJS.  
- APIs para consulta de preços de combustível.  
- Explicação sobre o cálculo do lucro líquido.  
