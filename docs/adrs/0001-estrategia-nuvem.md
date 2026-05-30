# ADR 0001: Estratégia de Nuvem e Escalabilidade

- **Status:** Aceito
- **Data:** 2026-05-30

## Contexto
A HealthSync exige alta disponibilidade, ingestão contínua de dados IoT e crescimento elástico do volume de consultas. O modelo tradicional em VMs dedicadas cria risco de subdimensionamento em picos e eleva o esforço operacional (Richards & Ford, 2020). Também é necessário reduzir o tempo de provisionamento e garantir conformidade com requisitos de segurança e privacidade.

## Decisão
Adotar **PaaS com Kubernetes gerenciado** e serviços de dados gerenciados. A escalabilidade será **horizontal**, usando autoscaling por métricas de CPU, latência e tamanho de filas de eventos. Ambientes críticos serão distribuídos em múltiplas zonas de disponibilidade com balanceamento de carga e backups automatizados.

## Alternativas consideradas
1. **IaaS com VMs tradicionais:** maior controle, porém alto esforço operacional, escalabilidade lenta e risco de inconsistência em picos.
2. **Serverless full stack:** elasticidade máxima, porém limitações de latência previsível, cold start e observabilidade para fluxos clínicos críticos.
3. **SaaS especializado para todo o domínio:** reduz operação, porém compromete a interoperabilidade e a evolução do core de domínio.

## Consequências
- **Positivas:** elasticidade rápida, menor overhead de operação, observabilidade integrada e melhor alinhamento com requisitos de disponibilidade.
- **Negativas:** dependência de plataforma gerenciada e necessidade de governança de custos (FinOps).

## Referências
- Richards, M., & Ford, N. (2020). *Fundamentals of Software Architecture*. O'Reilly Media.
- Newman, S. (2021). *Building Microservices* (2nd ed.). O'Reilly Media.
