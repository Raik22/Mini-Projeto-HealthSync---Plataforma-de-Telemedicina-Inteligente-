# ADR 0003: Modelo de Comunicação

- **Status:** Aceito
- **Data:** 2026-05-30

## Contexto
O sistema combina fluxos interativos (teleconsulta, prontuário) e ingestão massiva de telemetria (wearables). Comunicação totalmente síncrona gera acoplamento temporal e pode bloquear fluxos críticos durante picos. Comunicação totalmente assíncrona pode introduzir latência onde a decisão clínica exige resposta imediata (Newman, 2021).

## Decisão
Adotar um **modelo híbrido**:
- **Síncrono (REST):** para operações clínicas críticas e leitura imediata de dados do prontuário.
- **Assíncrono (eventos):** para ingestão de telemetria, análises de IA e envio de notificações.
- **Event Bus (Kafka):** como backbone para desacoplamento e reprocessamento seguro.

## Alternativas consideradas
1. **Síncrono para tudo:** baixa complexidade inicial, porém acoplamento e risco de cascata.
2. **Assíncrono para tudo:** alta resiliência, porém latência e maior complexidade de consistência eventual.

## Consequências
- **Positivas:** melhor equilíbrio entre latência e resiliência, escalabilidade para telemetria e redução de acoplamento.
- **Negativas:** necessidade de governança de eventos, versionamento de schemas e observabilidade distribuída.

## Referências
- Newman, S. (2021). *Building Microservices* (2nd ed.). O'Reilly Media.
- Kleppmann, M. (2017). *Designing Data-Intensive Applications*. O'Reilly Media.
