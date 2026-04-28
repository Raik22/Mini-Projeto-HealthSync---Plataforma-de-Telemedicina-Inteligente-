# ADR 0001: Adoção de Arquitetura Hexagonal para o Core da HealthSync

- **Status:** Aceito
- **Data:** 2026-04-28

## Contexto

A análise da Fase 1 revelou que o modelo N-Tier tradicional estava a gerar um acoplamento excessivo entre a lógica de negócio e os detalhes de persistência. Para um sistema de saúde que exige alta Interoperabilidade e escalabilidade para dados de sensores IoT, é vital que o domínio seja agnóstico a detalhes técnicos e frameworks (MARTIN, 2017).

## Decisão

Decidimos implementar o padrão de Portas e Adaptadores. O "Core" da aplicação conterá apenas as regras de negócio de telemedicina e monitorização. Toda a comunicação externa (Bases de Dados, API de IA, Wearables) será feita através de interfaces definidas pelo domínio (Ports) e implementadas pela infraestrutura (Adapters).

## Justificativa

- **Redução da Dívida Técnica:** Evita que a lógica médica fique "presa" a tecnologias específicas (ex: um banco SQL ou uma biblioteca de IA específica).
- **Evolução Facilitada:** Permite substituir fornecedores de wearables ou modelos de IA sem reescrever o motor de regras de diagnóstico.
- **Conformidade Técnica:** Alinha o projeto com a Regra de Dependência (Dependency Rule), onde o domínio não conhece a infraestrutura, mitigando os riscos de falhas sistêmicas apontados na revisão do Ciclo 1.
