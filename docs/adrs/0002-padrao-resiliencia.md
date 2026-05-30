# ADR 0002: Padrões de Resiliência

- **Status:** Aceito
- **Data:** 2026-05-30

## Contexto
O ecossistema de microsserviços da HealthSync está sujeito a falhas parciais, picos de carga e indisponibilidade de integrações externas. Em sistemas de saúde, falhas em cascata podem interromper consultas críticas. É necessário isolar dependências e garantir degradação controlada (Nygard, 2018).

## Decisão
Adotar um conjunto de padrões de resiliência composto por:
- **API Gateway** como ponto único de entrada, aplicando autenticação, rate limit e roteamento.
- **Circuit Breaker** entre serviços críticos para interromper falhas em cascata.
- **Bulkhead** para isolamento de recursos por domínio (teleconsulta, monitoramento, notificações).
- **Retries exponenciais com jitter** para chamadas idempotentes.

## Alternativas consideradas
1. **Somente retries:** simples, porém aumenta tempestades de requisições em incidentes.
2. **Service Mesh para resiliência completa:** robusto, porém maior complexidade operacional e curva de aprendizado.
3. **Fallbacks manuais sem circuit breaker:** dependente de implementação ad hoc e risco de inconsistência.

## Consequências
- **Positivas:** isolamento de falhas, melhor previsibilidade de recuperação e proteção de SLAs clínicos.
- **Negativas:** aumento de complexidade de configuração e necessidade de métricas consistentes para limiares de circuito.

## Referências
- Nygard, M. (2018). *Release It!* (2nd ed.). Pragmatic Bookshelf.
- Richards, M., & Ford, N. (2020). *Fundamentals of Software Architecture*. O'Reilly Media.
