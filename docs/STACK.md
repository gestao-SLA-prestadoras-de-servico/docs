# Stack Tecnológica

Esse documento contempla a stack tecnológica selecionada dentro de cada uma das suas respectivas áreas, levando em consideração arquitetura da apliação.

## Frontend

| Tech | Categoria | Justificativa |
| --- | --- | --- |
| Angular | Framework principal | O Angular dita uma arquitetura opinada e padronizada (opinionated), o que é excelente para sistemas corporativos, pois garante que todos os desenvolvedores sigam a mesma estrutura, tornando o código mais seguro, escalável e de fácil manutenção. |
| TailwindCSS | Estilização | Devido sua estilização ir diretamente na classe, facilita manter sempre o mesmo padrão relacionado a estética visual do sistema. |
| Zod | Validação e Schemas | A biblioteca Zod é especializada em validação de dados, permitindo a geração de mensagens de erro antes mesmo da requisição ir para o backend. Conta com uma estrutura fácil de configurar e traz a possibilidade de gerar tanto DTOs quanto Schemas que podem ser facilmente utilizados, além de eliminar a necessidade de duplicar a tipagem no TypeScript devido sua inferência estática de tipos. |

## Backend

| Tech | Categoria | Justificativa |
| --- | --- | --- |
| Java 21 (LTS) + Spring Boot | Framework principal | Exigência da disciplina e escolha ideal por ser uma plataforma corporativa madura e extremamente robusta, garantindo a segurança esperada para o FlowSLA. O ecossistema Spring acelera o desenvolvimento ao fornecer bibliotecas prontas para uso e suporte nativo integrado para persistência, segurança, mensageria e observabilidade. |
| PostgreSQL | Base de dados | Banco relacional robusto para os dados transacionais do domínio, garantindo controle de concorrência e integridade referencial. Destaca-se por permitir operações complexas e oferecer suporte nativo a campos JSONB, um recurso estratégico para o armazenamento de logs complexos e do histórico dinâmico de atendimentos dos SLAs. |
| Keycloak | Autenticação | Provedor de identidade externo (OAuth 2.1 / OIDC), desacoplando autenticação do código da aplicação e permitindo gestão centralizada de papéis. |

## Testes

| Tech | Categoria | Justificativa |
| --- | --- | --- |
| Cypress | Testes E2E | Além de ser facilmente configurável, também é muito confiável e traz consigo a possibilidade de observar os testes diante de uma interface gráfica, dessa forma tornando eles muito mais palpáveis e verificáveis, levando em consideração a visão do usuário final. |
| Testcontainers | Testes de integração | Permite que os testes de integração possuam determinadas configurações em cima de imagens Docker limpas (como uma imagem Postgres, por exemplo) e mantém o ciclo de vida diretamente ligado aos testes. |
| Spring Test (JUnit 5 + Mockito) | Testes de unitários no backend | Ferramentas padrão para testes no ecossistema Spring, oferecendo 100% de integração direta sem necessidade de configurações complexas. Serão utilizadas para a criação de testes unitários rápidos e isolados de dependências externas, com foco principal em garantir a exatidão da lógica de cálculo de SLA. |
| Jest | Testes unitários no frontend | Suporte oficial e excelente dentro do ecossistema Angular. |
| k6 | Testes de carga | Ferramenta de teste de carga escolhida por permitir script versionado em JavaScript e execução em contêiner, alinhada à necessidade de comprovar a escalabilidade do microsserviço. |

## Microsserviço

| Tech | Categoria | Justificativa |
| --- | --- | --- |
| Spring Boot | Framework principal | Permite isolar os altos recursos de CPU exigidos pelo processamento de mídia, além de manter a padronização tecnológica com o backend principal |
| RabbitMQ | Mensageria | Escolhido em vez de Kafka por o caso de uso do projeto ser fila de trabalho com roteamento e dead letter queue nativa, e não streaming de eventos com necessidade de replay. RabbitMQ atende ao requisito com menor complexidade operacional. |
| MinIO (compatível com S3) | Armazenamento de arquivos | Armazenamento de objetos para as evidências. Um banco relacional não é adequado para arquivos binários de grande volume: infla o backup e degrada o desempenho de consulta. A compatibilidade com a API S3 permite migração futura para um provedor de nuvem sem alteração de código. |
| Resilience4j | Resiliência do sistema | Implementação de padrões de resiliência (timeout, retry, circuit breaker) nas chamadas externas do sistema. |

## Infraestrutura e DevOps

| Tech | Categoria | Justificativa |
| --- | --- | --- |
| Docker e Docker Compose | Infra e separação de ambientes | O empacotamento em contêineres é uma exigência do projeto para garantir a total reprodutibilidade do sistema e simplificar o processo de deploy. A combinação com o Docker Compose permite orquestrar todos os serviços dependentes de forma ágil, gerando três ambientes isolados (desenvolvimento, testes e produção) facilmente executáveis em qualquer máquina. |
| GitHub Actions | CI/CD | Ferramenta escolhida por sua facilidade de configuração e integração nativa com o repositório do projeto. |
| Vercel | Deploy Frontend | Serviço gratuito que integra diretamente com o GitHub sem necessitar de nenhuma configuração. |
| A definir | Deploy Backend | — |
| A definir | Deploy Microsserviço | — |

## Observabilidade

| Tech | Categoria | Justificativa |
| --- | --- | --- |
| Prometheus + Grafana | Observabilidade e Coleta de métricas | Coleta de métricas e painel de observabilidade, integrados ao Spring Boot Actuator e Micrometer. |

