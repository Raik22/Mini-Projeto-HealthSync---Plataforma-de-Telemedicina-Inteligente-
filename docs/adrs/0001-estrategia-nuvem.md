# ADR 0001: Estratégia de Nuvem e Escalabilidade

- **Status:** Aceito
- **Data:** 2026-05-30

## Contexto
A HealthSync precisa suportar picos de demanda em teleconsultas e ingestão de dados IoT, mantendo disponibilidade 24/7 e conformidade com LGPD/HIPAA. A arquitetura em microsserviços exige implantação distribuída, com observabilidade, automação e capacidade de escalar sob demanda (RICHARDS & FORD, 2020).

## Decisão
Adotar uma estratégia **PaaS + Containers gerenciados** em nuvem pública (ex.: AWS), usando orquestração Kubernetes gerenciada (EKS) para os microsserviços e serviços gerenciados para dados e mensageria (RDS, MSK/SQS). A escalabilidade será **horizontal** para serviços stateless (Auto Scaling) e **vertical** quando necessário para bancos de dados, sempre com replicação multi-AZ.

## Consequências
### Benefícios
- **Elasticidade:** ajuste automático de capacidade para atender picos de teleconsulta e ingestão de sinais vitais.
- **Redução de risco operacional:** serviços gerenciados reduzem esforço de patching e manutenção.
- **Base sólida para resiliência:** multi-AZ e balanceamento distribuído mitigam falhas locais.

### Trade-offs
- **Custo variável:** o uso de serviços gerenciados pode elevar custos em cenários de alta carga.
- **Dependência do provedor:** configurações avançadas podem gerar lock-in parcial.
- **Complexidade de operação:** requer disciplina de observabilidade, IaC e governança de custos.

## Alternativas Consideradas
- **IaaS com VMs:** maior controle, porém maior esforço operacional e menor elasticidade.
- **Serverless puro:** excelente elasticidade, mas limitações para workloads de longa duração e latência previsível.
- **On-premises:** incompatível com a necessidade de escala rápida e alta disponibilidade global.

## Referências
- Richards, M., & Ford, N. (2020). *Fundamentals of Software Architecture*.
- Pressman, R. S. (2021). *Engenharia de Software: Uma Abordagem Profissional*.
