## Arquitetura de Pastas para o Projeto Fintech Pagu

Apresento a estrutura de pastas detalhada para o seu projeto **Pagu**, um sistema de pagamentos digitais. Esta organização foi pensada para promover a clareza, a escalabilidade e a colaboração, seguindo o padrão de microsserviços para o backend.

```
Pago/
├── backend/
│   ├── auth/                 # [MICS] Serviço de **autenticação** e **autorização** de usuários e outras aplicações. Gerencia tokens de acesso, sessões e permissões.
│   │   ├── src/              # Código fonte do serviço de autenticação.
│   │   └── config/           # Ficheiros de configuração específicos do serviço de autenticação.
│   ├── accounts/             # [MICS] Serviço de gestão de **contas digitais**. Responsável pela criação, consulta, fecho de contas, saldos e extratos.
│   │   ├── src/              # Código fonte do serviço de contas.
│   │   └── database/         # Scripts de migração e esquemas de base de dados para contas.
│   ├── transactions/         # [MICS] Serviço de **processamento de transações**. Lida com a iniciação, validação, roteamento e liquidação de pagamentos.
│   │   ├── src/              # Código fonte do serviço de transações.
│   │   └── listeners/        # Consumidores de mensagens para eventos de transação.
│   ├── merchants/            # [MICS] Serviço de gestão de **comerciantes** e parceiros. Abrange o cadastro, aprovação, configurações e liquidação de fundos para comerciantes.
│   │   ├── src/              # Código fonte do serviço de comerciantes.
│   │   └── api/              # Definições de API para integração de comerciantes.
│   ├── pfm/                  # [MICS] Serviço de **Personal Finance Management (PFM)**. Oferece funcionalidades como categorização de gastos, orçamentos, e relatórios financeiros pessoais.
│   │   ├── src/              # Código fonte do serviço PFM.
│   │   └── models/           # Modelos de Machine Learning para categorização, se aplicável.
│   ├── card/                 # [MICS] Serviço de **cartões**. Responsável pela emissão, ativação, bloqueio, gestão de BINs e tokenização de cartões (físicos e virtuais).
│   │   ├── src/              # Código fonte do serviço de cartões.
│   │   └── integrations/     # Código para integração com processadores de cartão e bandeiras.
│   ├── fraud/                # [MICS] Serviço de **prevenção e detecção de fraudes**. Inclui regras antifraude, modelos preditivos e sistemas de alerta.
│   │   ├── src/              # Código fonte do serviço de fraude.
│   │   └── rules/            # Definição das regras de negócio antifraude.
│   ├── kyc_aml/              # [MICS] Serviço de **KYC (Know Your Customer)** e **AML (Anti-Money Laundering)**. Gerencia a verificação de identidade, due diligence e monitoramento de transações para conformidade regulatória.
│   │   ├── src/              # Código fonte do serviço KYC/AML.
│   │   └── compliance/       # Documentação e regras de conformidade.
│   ├── external/             # [MICS] Serviço de **integrações externas**. Atua como um gateway para comunicação com terceiros (bancos legados, outros gateways de pagamento, bureaus de crédito).
│   │   ├── src/              # Código fonte do serviço externo.
│   │   └── clients/          # Clientes HTTP/SDKs para APIs de terceiros.
│   ├── notifications/        # [MICS] Serviço de **notificações**. Centraliza o envio de SMS, e-mails, push notifications e outras comunicações aos usuários.
│   │   ├── src/              # Código fonte do serviço de notificações.
│   │   └── templates/        # Templates para e-mails e mensagens.
│   ├── common/               # Contém código, bibliotecas e modelos de dados **comuns** partilhados entre os diversos microsserviços.
│   │   ├── lib/              # Bibliotecas utilitárias partilhadas.
│   │   └── models/           # Modelos de dados globais (ex: User, Money).
│   └── docs/                 # Documentação específica do backend (ex: diagramas de sequência de microsserviços).
├── frontend/
│   ├── mobile/               # Contém o código das **aplicações móveis**.
│   │   ├── android/          # Código fonte da aplicação **Android**.
│   │   └── ios/              # Código fonte da aplicação **iOS**.
│   └── web/                  # Contém o código da **aplicação web**.
├── infrastructure/
│   ├── database/             # Scripts e configurações para as **bases de dados**. Inclui DDLs, scripts de migração (ex: Flyway, Liquibase) e configurações de conexão.
│   ├── messaging/            # Configurações do sistema de **mensagens** (ex: Kafka topics, Consumer Groups).
│   ├── monitoring/           # Configurações de **monitorização** e alertas (ex: Prometheus, Grafana dashboards, ELK Stack).
│   ├── deployment/           # Scripts e configurações para o **deploy** das aplicações (ex: Kubernetes manifests, Terraform IaC, scripts de CI/CD).
│   ├── vpc/                  # Configurações de rede (VPC, subnets, security groups) se usar cloud provider.
│   └── secrets/              # Gestão de segredos e credenciais (ex: HashiCorp Vault, AWS Secrets Manager).
├── docs/                     # **Documentação** geral do projeto.
│   ├── api/                  # Documentação das **APIs** (geralmente OpenAPI/Swagger), incluindo as APIs de todos os microsserviços.
│   ├── architecture/         # Documentação da **arquitetura** de alto nível do sistema (diagramas, decisões de design).
│   ├── regulatory/           # Documentação sobre os **requisitos regulatórios** e compliance.
│   ├── onboarding/           # Guias para novos membros da equipe.
│   └── roadmap/              # Visão geral do roadmap do produto.
├── tests/
│   ├── unit/                 # **Testes unitários** para componentes e funções individuais de cada microsserviço/frontend.
│   ├── integration/          # **Testes de integração** para verificar a comunicação entre os componentes e microsserviços.
│   ├── e2e/                  # **Testes end-to-end (ponta a ponta)** para simular o fluxo completo do usuário através do sistema.
│   └── performance/          # Testes de carga e performance (ex: JMeter, K6).
├── .github/                  # Configurações de CI/CD (Continuous Integration/Continuous Deployment) para GitHub Actions ou outros pipelines.
├── .gitignore                # Arquivo de configuração do Git para ignorar ficheiros e pastas que não devem ser versionados.
├── LICENSE                   # Licença de uso do código do projeto.
├── README.md                 # Descrição geral do projeto, como configurá-lo e executá-lo.
├── docker-compose.yml        # Ficheiro para orquestração de containers Docker em ambiente de desenvolvimento.
├── Makefile                  # Scripts úteis para tarefas comuns de desenvolvimento (build, run, test).
└── CONTRIBUTING.md           # Guia para contribuições ao projeto.
```
