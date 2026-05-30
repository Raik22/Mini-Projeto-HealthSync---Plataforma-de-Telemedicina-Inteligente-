# SAD – HealthSync (Fase 4)

## 1. Introdução
Este Software Architecture Document (SAD) descreve a arquitetura alvo da HealthSync na evolução para cloud e microsserviços. O documento consolida decisões do ciclo atual e descreve o estado arquitetural esperado na Fase 4, com foco em escalabilidade, resiliência e interoperabilidade.

## 2. Visão executiva
A HealthSync integra teleconsultas, monitoramento de sinais vitais via wearables e análise preditiva por IA. O objetivo é reduzir a fragmentação do cuidado médico, garantindo acesso contínuo a dados clínicos, alertas em tempo real e apoio à decisão médica.

## 3. Stakeholders
- **Pacientes:** acesso remoto a consultas e acompanhamento contínuo.
- **Profissionais de saúde:** tomada de decisão clínica baseada em dados e histórico consolidado.
- **Equipe de operações:** disponibilidade 24/7 e observabilidade do ecossistema.
- **Compliance/LGPD:** governança, privacidade e integridade de dados sensíveis.

## 4. Requisitos e RNFs priorizados
- **Segurança (LGPD/HIPAA):** proteção de dados sensíveis e conformidade legal.
- **Disponibilidade:** operação 24/7 para suporte a situações críticas.
- **Escalabilidade:** ingestão de grandes volumes de dados de sensores.
- **Integridade de dados:** confiabilidade para diagnósticos e prescrições.
- **Interoperabilidade:** integração com diferentes fabricantes de wearables e APIs externas.

## 5. Visão de arquitetura
### 5.1 Estilo arquitetural
O core do domínio adota **Arquitetura Hexagonal** (Ports and Adapters) para garantir baixo acoplamento e alta testabilidade. Os serviços são distribuídos em **microsserviços**, isolando responsabilidades e permitindo evolução independente.

### 5.2 Visão de containers
O ecossistema é composto por um gateway de API, serviços de teleconsulta, prontuário, monitoramento de IoT, diagnóstico por IA e notificações. O fluxo clínico principal é síncrono (consulta, prontuário), enquanto telemetria e alertas seguem fluxo assíncrono por eventos.

- Diagrama de contexto: [docs/diagrams/01-diagrama-contexto.md](../diagrams/01-diagrama-contexto.md)
- Diagrama de containers: [docs/diagrams/02-diagrama-containers.md](../diagrams/02-diagrama-containers.md)

## 6. Estratégia de cloud e implantação
A estratégia adota **PaaS com Kubernetes gerenciado**, bancos de dados gerenciados e observabilidade centralizada. A escalabilidade é **horizontal** com autoscaling por métricas de uso e filas de eventos. A decisão completa está documentada no [ADR 0001](../adrs/0001-estrategia-nuvem.md).

## 7. Resiliência e continuidade
O sistema utiliza **API Gateway**, **circuit breaker**, **bulkheads** por domínio e **retries exponenciais**. Serviços críticos possuem timeout, fallback e políticas de isolamento. A decisão está registrada no [ADR 0002](../adrs/0002-padrao-resiliencia.md).

## 8. Modelo de comunicação
A comunicação é **híbrida**: síncrona para operações clínicas críticas e assíncrona para ingestão de telemetria e notificações. Eventos são publicados em um barramento (Kafka) para desacoplamento. Justificativas e trade-offs estão no [ADR 0003](../adrs/0003-modelo-comunicacao.md).

## 9. Riscos principais e mitigação
- **Falha de serviço crítico:** mitigada com circuit breakers, replicação e rollback de releases.
- **Picos de tráfego em telemetria:** mitigados com filas, autoscaling e processamento por lotes.
- **Compliance e vazamento de dados:** mitigados com criptografia, auditoria e segregação de acesso.

## 10. Referências
- Pressman, R. S. (2021). *Engenharia de Software: Uma Abordagem Profissional*. McGraw Hill.
- Richards, M., & Ford, N. (2020). *Fundamentals of Software Architecture*. O'Reilly Media.
- Martin, R. C. (2017). *Clean Architecture*. Prentice Hall.
- C4 Model for Software Architecture. https://c4model.com/
- Architecture Decision Records (ADRs). https://adr.github.io/
