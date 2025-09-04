# Desafio de Projeto: Provisionando um Banco de Dados SQL no Microsoft Azure 

Repositório criado para documentar a execução do Desafio de Projeto da [DIO](https://www.dio.me/) sobre a configuração de uma instância de Banco de Dados na plataforma Microsoft Azure.

## 📝 Descrição do Desafio

O objetivo deste laboratório foi aplicar os conhecimentos adquiridos sobre os serviços de dados do Azure, focando especificamente na criação e configuração de uma Instância Gerenciada de SQL do Azure. Este repositório serve como um guia de consulta, consolidando o passo a passo do processo, além de resumos e anotações pertinentes para futuras implementações.

## 🎯 Objetivos de Aprendizagem Consolidados

Ao realizar este desafio, pude aprofundar minhas habilidades em:

- **Aplicação de Conceitos de Banco de Dados em Nuvem:** Implementei uma solução de PaaS (Plataforma como Serviço) para banco de dados, compreendendo na prática suas vantagens.
- **Documentação Técnica Estruturada:** Elaborei este documento para registrar o processo de forma clara e lógica.
- **Uso do GitHub para Documentação:** Utilizei o GitHub como portfólio e ferramenta para compartilhar o conhecimento adquirido.

---

## ⚙️ Passo a Passo da Criação da Instância SQL

A seguir, apresento as etapas que segui para provisionar a Instância Gerenciada de SQL do Azure, utilizando o portal e a documentação oficial como referência.

### 1. Criação do Grupo de Recursos (Resource Group)

Como boa prática, o primeiro passo foi criar um novo Grupo de Recursos para isolar e gerenciar todos os componentes associados à nossa instância de banco de dados.

- **Nome do Grupo de Recursos:** `rg-dio-desafio-sql`
- **Região:** `Brazil South` (Sul do Brasil)

### 2. Configuração da Instância Gerenciada de SQL

A Instância Gerenciada de SQL do Azure é um serviço de banco de dados inteligente e escalonável na nuvem. Ela combina a maior compatibilidade com o mecanismo do SQL Server com os benefícios de uma PaaS totalmente gerenciada.

#### **Configurações Básicas:**

- **Nome da Instância Gerenciada:** `sqlinstance-dio-desafio` (nomes devem ser globalmente únicos)
- **Região:** `Brazil South` (Sul do Brasil)
- **Computação e Armazenamento:** Para fins de estudo, selecionei a configuração mínima viável para manter os custos baixos. É importante notar que este recurso tem um custo mais elevado que um Banco de Dados SQL simples.
- **Autenticação:** Defini um login e uma senha de administrador do SQL. Essas credenciais serão usadas para acessar e gerenciar a instância após a criação.

#### **Configurações de Rede (Networking):**

A Instância Gerenciada requer uma **Rede Virtual (VNet)** e uma **sub-rede dedicada** para operar de forma segura e isolada.

1.  **Criação de uma nova VNet:** Criei uma nova rede virtual para hospedar a instância.
    -   **Nome da VNet:** `vnet-sqlinstance-dio`
2.  **Criação de uma Sub-rede Dedicada:** Dentro da VNet, configurei uma sub-rede exclusiva para a instância gerenciada, conforme exigido pelo Azure.

#### **Configurações de Segurança:**

Nesta etapa, configurei as regras para permitir o acesso à instância.

- **Permitir acesso do ponto de extremidade público:** Habilitei esta opção para poder me conectar à instância a partir da minha máquina local pela internet. Por padrão, o acesso é apenas privado, dentro da VNet.
- **Permitir acesso de:** Configurei as regras de firewall no Grupo de Segurança de Rede (NSG) para liberar o acesso na porta `3342` (porta do ponto de extremidade público) a partir do meu endereço IP.

### 3. Revisão e Implantação

Após revisar todas as configurações, iniciei o processo de implantação. **É importante notar que a criação de uma Instância Gerenciada de SQL é um processo demorado**, podendo levar várias horas para ser concluído. O Azure precisa provisionar e configurar um cluster de VMs dedicado nos bastidores.

Após a conclusão, a instância estava pronta para ser acessada através de ferramentas como o SQL Server Management Studio (SSMS) ou o Azure Data Studio, utilizando o nome do host do ponto de extremidade público e as credenciais de administrador definidas.

---

## 💡 Resumos, Anotações e Dicas

- **O que é uma Instância Gerenciada (Managed Instance)?** É uma opção de PaaS que oferece quase 100% de compatibilidade com o SQL Server on-premises. É ideal para empresas que querem migrar suas aplicações existentes para a nuvem com o mínimo de alteração no código do banco de dados, aproveitando recursos como backups automáticos, patching e alta disponibilidade.

- **Diferença entre Banco de Dados SQL e Instância Gerenciada:**
    - **Banco de Dados SQL do Azure:** É um banco de dados como serviço (DBaaS), ideal para novas aplicações nativas da nuvem. Você gerencia o banco de dados individualmente.
    - **Instância Gerenciada de SQL:** É uma instância completa do SQL Server na nuvem. Você obtém recursos no nível da instância (como SQL Agent, Service Broker) que não estão disponíveis no Banco de Dados SQL. É a melhor opção para migração (lift-and-shift).

- **Dica sobre a VNet:** A Rede Virtual é o componente mais crítico na configuração. A sub-rede da Instância Gerenciada não pode conter nenhum outro serviço e deve ser delegada ao serviço `Microsoft.Sql/managedInstances`. O portal do Azure geralmente cuida disso quando você cria uma nova VNet durante o provisionamento.

- **Atenção ao Custo:** A Instância Gerenciada é um recurso poderoso e, consequentemente, mais caro que outras opções de banco de dados. Para estudos, lembre-se de **excluir o recurso** (e o Grupo de Recursos associado) após a conclusão para evitar cobranças inesperadas.

## 🏁 Conclusão

Este desafio foi fundamental para compreender o processo de provisionamento de um serviço de dados robusto no Azure. A configuração da Instância Gerenciada de SQL, especialmente a parte de rede, destacou a importância da segurança e do isolamento em ambientes de nuvem. A experiência demonstrou o poder do modelo PaaS, que abstrai grande parte da complexidade de infraestrutura e permite focar na gestão dos dados.

## 📚 Recursos Úteis

-   **Documentação Oficial da Microsoft:** [Início Rápido: Criar uma Instância Gerenciada de SQL do Azure](https://learn.microsoft.com/pt-br/azure/azure-sql/managed-instance/instance-create-quickstart)
-   [DIO - Formação Microsoft Azure](https://www.dio.me/)
