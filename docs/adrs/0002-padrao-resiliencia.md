# ADR 0002: Padrões de Resiliência

- **Status:** Aceito
- **Data:** 2026-05-30

## Contexto
A HealthSync depende de múltiplos microsserviços e integrações externas (IA e wearables). Falhas em cascata ou picos de tráfego podem comprometer consultas críticas. A literatura recomenda padrões explícitos de resiliência para sistemas distribuídos (RICHARDS & FORD, 2020).

## Decisão
Adotar um **API Gateway** como ponto de controle de entrada e aplicar os padrões **Circuit Breaker**, **Bulkhead** e **Retry/Timeout** nos serviços críticos. O gateway será responsável por autenticação, rate limiting e roteamento. Os microsserviços utilizarão circuit breakers por dependência, bulkheads por pool de conexão e políticas de timeout consistentes.

## Consequências
### Benefícios
- **Isolamento de falhas:** circuit breakers evitam propagação de indisponibilidade.
- **Proteção contra picos:** rate limiting e bulkheads preservam a capacidade de serviços essenciais.
- **Recuperação previsível:** retries controlados e timeouts reduzem latência extrema.

### Trade-offs
- **Maior complexidade:** configuração e observabilidade são mais exigentes.
- **Overhead de latência:** políticas de resiliência adicionam camadas de processamento.
- **Necessidade de monitoramento contínuo:** tuning inadequado pode gerar falsos positivos.

## Alternativas Consideradas
- **Resiliência apenas na infraestrutura (LB/Auto Scaling):** insuficiente para falhas lógicas e degradação de dependências.
- **Retries indiscriminados:** risco de tempestade de requisições e aumento de latência.

## Referências
- Richards, M., & Ford, N. (2020). *Fundamentals of Software Architecture*.
- Pressman, R. S. (2021). *Engenharia de Software: Uma Abordagem Profissional*.
