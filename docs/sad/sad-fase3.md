# SAD — HealthSync (Fase 3: Arquitetura alvo da Fase 4)

## 1. Visão executiva
A HealthSync oferece teleconsultas, monitoramento de pacientes e diagnósticos assistidos por IA em um ecossistema único. Este SAD (entregue na Fase 3) descreve a **arquitetura alvo da Fase 4**, evoluída para Cloud e microsserviços, visando alta disponibilidade, segurança e escalabilidade, preservando a integridade dos dados clínicos.

## 2. Escopo do sistema
- Atendimento remoto (teleconsulta) e agendamento.
- Prontuário eletrônico integrado.
- Monitoramento contínuo via wearables.
- Diagnóstico assistido por IA e alertas clínicos.
- Notificações e comunicação com pacientes e equipes médicas.

## 3. Stakeholders
- **Pacientes:** acesso seguro e contínuo às consultas e histórico.
- **Médicos/Clínicas:** disponibilidade, performance e confiabilidade dos dados.
- **Operações/DevOps:** estabilidade, observabilidade e governança de custos.
- **Compliance/LGPD:** proteção e rastreabilidade de dados sensíveis.

## 4. Requisitos de qualidade (priorizados)
- **Segurança e conformidade (LGPD/HIPAA).**
- **Disponibilidade 24/7** para atendimento crítico.
- **Escalabilidade horizontal** para picos de teleconsulta e IoT.
- **Integridade e consistência de dados clínicos.**
- **Interoperabilidade** com APIs externas e dispositivos.

## 5. Restrições e premissas
- Uso de nuvem pública com serviços gerenciados.
- Microssserviços seguindo arquitetura hexagonal no core de negócio.
- Integração com APIs externas de IA e dispositivos.
- Observabilidade completa (logs, métricas, tracing).

## 6. Visões arquiteturais
### 6.1 Visão de contexto
A plataforma conecta pacientes, médicos e dispositivos a um ecossistema de serviços internos, expostos via API Gateway, com integrações externas para IA e wearables.

### 6.2 Visão de containers (C4 Nível 2)
**Serviços principais:**
- **API Gateway:** autenticação, roteamento, rate limiting.
- **Serviço de Autenticação:** identidade e tokens.
- **Serviço de Teleconsulta:** agenda, sessões e prescrições.
- **Serviço de Prontuário:** dados clínicos e histórico.
- **Serviço de Monitoramento IoT:** ingestão e processamento de sinais vitais.
- **Serviço de Diagnóstico por IA:** apoio a laudos e alertas.
- **Serviço de Notificações:** comunicação omnichannel.

### 6.3 Visão de implantação
- **Kubernetes gerenciado (EKS)** para serviços stateless.
- **RDS PostgreSQL** para dados transacionais.
- **Timeseries DB** para telemetria.
- **Object Storage** para laudos e anexos.
- **Event Bus** para comunicação assíncrona.

## 7. Modelo de comunicação
- **Síncrono:** REST/gRPC para operações com resposta imediata (teleconsulta, prontuário, autenticação).
- **Assíncrono:** eventos para telemetria e notificações, reduzindo acoplamento e absorvendo picos.

## 8. Persistência e dados
- **Dados transacionais:** PostgreSQL (prontuários, agenda).
- **Telemetria:** banco de séries temporais.
- **Arquivos e anexos:** object storage com versionamento.

## 9. Segurança e conformidade
- OAuth2/OpenID Connect no gateway.
- Criptografia em trânsito (TLS) e em repouso.
- Logs de auditoria para acessos a dados sensíveis.
- Segregação de dados por tenant quando aplicável.

## 10. Resiliência e observabilidade
- Padrões **Circuit Breaker** e **Bulkhead** nos serviços críticos.
- Timeouts e retries controlados.
- Monitoramento com métricas, tracing distribuído e alertas.

## 11. Riscos e mitigação
- **Picos inesperados:** auto scaling e filas assíncronas.
- **Falhas de dependências externas:** circuit breakers e fallback degradado.
- **Lock-in de provedor:** abstrações de infraestrutura e IaC portátil.

## 12. ADRs relacionados
- [ADR 0001 — Estratégia de Nuvem e Escalabilidade](../adrs/0001-estrategia-nuvem.md)
- [ADR 0002 — Padrões de Resiliência](../adrs/0002-padrao-resiliencia.md)
- [ADR 0003 — Modelo de Comunicação](../adrs/0003-modelo-comunicacao.md)

## 13. Referências
- Richards, M., & Ford, N. (2020). *Fundamentals of Software Architecture*.
- Pressman, R. S. (2021). *Engenharia de Software: Uma Abordagem Profissional*.
- C4 Model for Software Architecture. https://c4model.com/
