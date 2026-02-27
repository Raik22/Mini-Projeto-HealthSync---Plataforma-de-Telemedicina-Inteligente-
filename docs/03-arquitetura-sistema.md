# 03 – Arquitetura do Sistema

## 3.1 Estilo Arquitetural

O **HealthSync** adota uma arquitetura de **Microsserviços** combinada com o padrão **API Gateway**, proporcionando:

- **Escalabilidade independente** de cada serviço.
- **Isolamento de falhas** entre módulos.
- **Implantação contínua** sem impacto global no sistema.
- **Manutenibilidade** e evolução tecnológica por serviço.

## 3.2 Diagrama de Arquitetura

```
                          +-----------------+
   Clientes               |   API Gateway   |
   (Web / Mobile)  -----> |  (Authn/Authz)  |
                          +-------+---------+
                                  |
          +-----------+-----------+-----------+-----------+
          |           |           |           |           |
  +-------v---+ +-----v-----+ +--v--------+ +v----------+ +----------+
  | Serviço   | | Serviço   | | Serviço   | | Serviço   | | Serviço  |
  | Usuários  | | Consultas | | Prontuário| | Prescrição| |  IoT /   |
  | (Auth)    | | (Video)   | | (EHR)     | | Digital   | | Wearable |
  +-----------+ +-----------+ +-----------+ +-----------+ +----------+
          |           |           |           |           |
          +-----+-----+-----------+-----------+-----+-----+
                |                                   |
        +-------v-------+                   +-------v-------+
        |  Message Bus  |                   |  Banco de     |
        |  (Event/MQTT) |                   |  Dados        |
        +---------------+                   +---------------+
```

> **[TODO]** Substitua o diagrama ASCII pelo diagrama arquitetural real (ex.: diagrama C4 nível 2 ou diagrama de implantação UML).

## 3.3 Camadas da Arquitetura

| Camada | Responsabilidade |
|--------|-----------------|
| **Apresentação** | Interface Web (React/Angular) e aplicativo móvel (React Native / Flutter) |
| **API Gateway** | Roteamento, autenticação JWT, rate limiting e logging centralizado |
| **Negócio (Microsserviços)** | Lógica de domínio encapsulada por contexto (usuários, consultas, EHR, prescrições, IoT) |
| **Mensageria** | Comunicação assíncrona entre serviços via Kafka ou RabbitMQ |
| **Dados** | Banco relacional (PostgreSQL) para dados transacionais; MongoDB para prontuários; Redis para cache |
| **Infraestrutura** | Kubernetes (K8s) em nuvem (AWS / Azure / GCP) com CI/CD automatizado |

## 3.4 Decisões Arquiteturais

| ID | Decisão | Justificativa |
|----|---------|---------------|
| DA-01 | Microsserviços | Permite escalar e evoluir cada domínio independentemente |
| DA-02 | API Gateway centralizado | Simplifica autenticação, logging e controle de tráfego |
| DA-03 | JWT para autenticação | Stateless, performático e amplamente suportado |
| DA-04 | PostgreSQL para dados transacionais | ACID, maturidade e suporte a dados relacionais de saúde |
| DA-05 | MongoDB para prontuários | Flexibilidade de esquema para dados clínicos variados |
| DA-06 | Kafka para mensageria | Alta throughput para eventos de IoT e notificações |
| DA-07 | Kubernetes para orquestração | Auto-scaling, resiliência e gestão de contêineres |

> **[TODO]** Documente decisões adicionais relevantes para o seu projeto.

## 3.5 Padrões de Projeto Adotados

- **Repository Pattern** – abstração do acesso a dados em cada microsserviço.
- **CQRS** (Command Query Responsibility Segregation) – separação de leitura e escrita no módulo de prontuário.
- **Event Sourcing** – rastreabilidade de eventos clínicos no histórico do paciente.
- **Circuit Breaker** – resiliência nas chamadas entre serviços (ex.: Resilience4j / Hystrix).

---

*[← 02 – Visão Geral do Sistema](02-visao-geral-sistema.md) | [04 – Componentes e Módulos →](04-componentes.md)*
