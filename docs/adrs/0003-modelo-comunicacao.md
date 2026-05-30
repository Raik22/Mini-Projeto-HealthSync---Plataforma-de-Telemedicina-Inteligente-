# ADR 0003: Modelo de Comunicação

- **Status:** Aceito
- **Data:** 2026-05-30

## Contexto
A plataforma possui casos de uso com resposta imediata (teleconsulta, autenticação) e fluxos intensivos de eventos (telemetria IoT, notificações). Um único estilo de comunicação não atende ambos sem comprometer desempenho ou confiabilidade (RICHARDS & FORD, 2020).

## Decisão
Adotar um **modelo híbrido**:
- **Síncrono (REST/gRPC):** para operações de consulta e comandos que exigem resposta imediata (agendamento, prontuário, autenticação).
- **Assíncrono (Event Bus):** para ingestão de telemetria, alertas e notificações, garantindo desacoplamento e absorção de picos.

## Consequências
### Benefícios
- **Baixa latência onde importa:** fluxos críticos permanecem síncronos.
- **Escalabilidade e desacoplamento:** eventos absorvem picos sem bloquear serviços.
- **Resiliência ampliada:** consumidores podem falhar sem interromper o produtor.

### Trade-offs
- **Complexidade operacional:** necessidade de broker e observabilidade distribuída.
- **Consistência eventual:** eventos podem introduzir atraso em atualizações.
- **Contratos de mensagens:** exige governança para evitar quebra de compatibilidade.

## Alternativas Consideradas
- **Síncrono exclusivo:** simples, porém frágil a picos e acoplamento alto.
- **Assíncrono exclusivo:** escalável, mas inadequado para consultas de baixa latência.

## Referências
- Richards, M., & Ford, N. (2020). *Fundamentals of Software Architecture*.
- Pressman, R. S. (2021). *Engenharia de Software: Uma Abordagem Profissional*.
