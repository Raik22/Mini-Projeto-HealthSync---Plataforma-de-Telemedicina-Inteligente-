# 08 – Implantação

## 8.1 Visão Geral da Infraestrutura

O **HealthSync** é implantado em nuvem pública utilizando uma abordagem **Cloud-Native**, com contêineres orquestrados pelo **Kubernetes**.

```
+-----------------------------+
|       Usuários              |
|  (Web Browser / App Mobile) |
+-------------+---------------+
              |
+-------------v---------------+
|       CDN / Load Balancer   |
|   (AWS CloudFront / ALB)    |
+-------------+---------------+
              |
+-------------v---------------+
|        API Gateway          |
|  (Kong / AWS API Gateway)   |
+-----+-------+-------+-------+
      |       |       |
  +---v--+ +--v---+ +-v------+
  | MS 1 | | MS 2 | |  MS N  |  <- Pods no Kubernetes
  +---+--+ +--+---+ +-+------+
      |       |       |
  +---v-------v-------v------+
  |    Banco de Dados         |
  |  PostgreSQL | MongoDB     |
  |  Redis (cache)            |
  +---------------------------+
```

> **[TODO]** Substitua pelo diagrama de implantação real do projeto.

---

## 8.2 Ambientes

| Ambiente | Finalidade | URL Base |
|----------|-----------|----------|
| **Desenvolvimento** | Desenvolvimento local dos times | `http://localhost:3000` |
| **Homologação (Staging)** | Testes de integração e validação | `https://staging.healthsync.com` |
| **Produção** | Ambiente de uso real dos usuários | `https://app.healthsync.com` |

---

## 8.3 Tecnologias de Infraestrutura

| Componente | Tecnologia |
|-----------|------------|
| Contêineres | Docker |
| Orquestração | Kubernetes (EKS / AKS / GKE) |
| CI/CD | GitHub Actions / GitLab CI |
| Registro de imagens | Docker Hub / AWS ECR |
| Banco relacional | PostgreSQL (AWS RDS / Azure Database) |
| Banco de documentos | MongoDB Atlas |
| Cache | Redis (ElastiCache) |
| Armazenamento de objetos | AWS S3 / Azure Blob Storage |
| Monitoramento | Prometheus + Grafana |
| Logs centralizados | ELK Stack (Elasticsearch, Logstash, Kibana) |
| Rastreamento distribuído | Jaeger / Zipkin |
| Secrets management | HashiCorp Vault / AWS Secrets Manager |

---

## 8.4 Pipeline de CI/CD

```
Commit/PR
   |
   v
+--+-------------+
| Lint & Tests   |  <- Testes unitários e de integração
+--+-------------+
   |
   v
+--+-------------+
| Build Docker   |  <- Build da imagem e push para o registry
| Image          |
+--+-------------+
   |
   v
+--+-------------+
| Deploy         |  <- Deploy automático em Staging
| Staging        |
+--+-------------+
   |
   v
+--+-------------+
| Smoke Tests    |  <- Testes de fumaça no ambiente de staging
+--+-------------+
   |  (aprovação manual para produção)
   v
+--+-------------+
| Deploy         |  <- Deploy em Produção (Rolling Update)
| Produção       |
+----------------+
```

---

## 8.5 Escalabilidade e Alta Disponibilidade

- **Horizontal Pod Autoscaler (HPA):** escala automática de pods com base em CPU/memória.
- **Multi-AZ:** bancos de dados e serviços críticos replicados em múltiplas zonas de disponibilidade.
- **Health Checks:** liveness e readiness probes em todos os microsserviços.
- **Rolling Updates:** atualizações sem downtime utilizando estratégia `RollingUpdate` no Kubernetes.
- **Backup:** backups automáticos diários dos bancos de dados com retenção de 30 dias.

---

> **[TODO]** Detalhe as configurações de recursos (CPU/memória) e políticas de auto-scaling para cada serviço.

---

*[← 07 – Segurança](07-seguranca.md) | [09 – Casos de Uso →](09-casos-uso.md)*
