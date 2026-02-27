# 07 – Segurança

## 7.1 Autenticação e Autorização

### 7.1.1 Autenticação

O sistema utiliza **JWT (JSON Web Token)** para autenticação stateless:

- **Access Token:** validade de **1 hora**; transmitido no header `Authorization: Bearer <token>`.
- **Refresh Token:** validade de **7 dias**; armazenado em cookie `HttpOnly` e `Secure`.
- Tokens expirados ou inválidos são rejeitados com `401 Unauthorized`.

### 7.1.2 Autorização (RBAC)

O controle de acesso é baseado em papéis (**Role-Based Access Control**):

| Papel | Permissões |
|-------|------------|
| `PATIENT` | Visualizar próprio perfil, histórico e consultas |
| `DOCTOR` | Gerenciar consultas, criar prontuários e prescrições |
| `ADMIN` | Gerenciar todos os usuários e configurações do sistema |
| `DEVICE` | Publicar métricas IoT (autenticação por certificado mTLS) |

---

## 7.2 Proteção de Dados (LGPD)

O sistema está em conformidade com a **Lei Geral de Proteção de Dados (LGPD – Lei nº 13.709/2018)**:

| Requisito LGPD | Implementação |
|----------------|---------------|
| Consentimento do titular | Aceite explícito na criação da conta, registrado com timestamp |
| Minimização de dados | Coleta apenas dados estritamente necessários |
| Direito de acesso | Endpoint `GET /users/{id}/data-export` para exportação dos dados |
| Direito ao esquecimento | Endpoint `DELETE /users/{id}` com anonimização dos dados |
| Portabilidade | Exportação em formato JSON/CSV sob demanda |
| Notificação de incidentes | Processo documentado de resposta a incidentes em 72 horas |

---

## 7.3 Criptografia

| Dado | Mecanismo |
|------|-----------|
| Senhas | Hashing com **bcrypt** (custo mínimo 12) |
| CPF, dados pessoais sensíveis | Criptografia em repouso com **AES-256** |
| Comunicação entre clientes e API | **TLS 1.2+** obrigatório |
| Comunicação entre microsserviços | **mTLS** (mutual TLS) com certificados internos |
| Dados em banco de dados | Criptografia de volume (AWS KMS / Azure Key Vault) |
| Prescrições digitais | Assinatura digital com **RSA-2048** |

---

## 7.4 Proteção contra Vulnerabilidades Comuns (OWASP Top 10)

| Vulnerabilidade | Controle Implementado |
|----------------|-----------------------|
| Injeção (SQL/NoSQL) | ORM com queries parametrizadas; sanitização de entrada |
| Autenticação quebrada | JWT com expiração curta; bloqueio após tentativas falhas |
| Exposição de dados sensíveis | TLS obrigatório; mascaramento de dados em logs |
| XXE | Desabilitado no parser XML |
| Controle de acesso quebrado | RBAC validado no API Gateway e em cada serviço |
| Configurações incorretas | Hardening de contêineres; secrets via variáveis de ambiente |
| XSS | CSP headers; sanitização de saídas no front-end |
| Deserialização insegura | Validação de schema nas entradas (ex.: Zod, Joi, Pydantic) |
| Logging e monitoramento insuficientes | Logs centralizados (ELK Stack); alertas em tempo real |

---

## 7.5 Auditoria e Rastreabilidade

- Todos os acessos a dados clínicos são registrados em log de auditoria imutável.
- Logs contêm: `usuário`, `ação`, `recurso acessado`, `timestamp`, `IP de origem`.
- Logs são retidos por no mínimo **5 anos** (conforme Resolução CFM).
- Acesso aos logs de auditoria é restrito ao papel `ADMIN`.

---

> **[TODO]** Documente controles de segurança adicionais específicos do seu ambiente.

---

*[← 06 – APIs e Interfaces](06-apis.md) | [08 – Implantação →](08-implantacao.md)*
