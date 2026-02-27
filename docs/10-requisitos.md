# 10 – Requisitos

## 10.1 Requisitos Funcionais (RF)

| ID | Requisito | Prioridade |
|----|-----------|-----------|
| RF-01 | O sistema deve permitir o cadastro de pacientes com CPF, nome, e-mail e data de nascimento. | Alta |
| RF-02 | O sistema deve permitir o cadastro de médicos com CRM, especialidade e grade de disponibilidade. | Alta |
| RF-03 | O sistema deve autenticar usuários via e-mail e senha, emitindo token JWT. | Alta |
| RF-04 | O sistema deve permitir que pacientes agendem consultas com médicos disponíveis. | Alta |
| RF-05 | O sistema deve realizar consultas médicas via videochamada integrada. | Alta |
| RF-06 | O sistema deve permitir ao médico registrar diagnóstico, prescrição e observações no prontuário. | Alta |
| RF-07 | O sistema deve armazenar o histórico clínico completo do paciente (EHR). | Alta |
| RF-08 | O sistema deve emitir prescrições digitais com assinatura eletrônica do médico. | Alta |
| RF-09 | O sistema deve receber e armazenar métricas de dispositivos IoT/wearables associados ao paciente. | Média |
| RF-10 | O sistema deve alertar o médico quando métricas do paciente estiverem fora dos limites normais. | Média |
| RF-11 | O sistema deve enviar lembretes de consulta por e-mail e SMS ao paciente e ao médico. | Média |
| RF-12 | O sistema deve permitir o cancelamento de consultas com antecedência mínima de 2 horas. | Média |
| RF-13 | O sistema deve permitir ao paciente exportar seus dados pessoais conforme exigido pela LGPD. | Alta |
| RF-14 | O sistema deve permitir ao administrador gerenciar usuários e visualizar relatórios. | Média |

> **[TODO]** Adicione requisitos funcionais específicos do seu projeto.

---

## 10.2 Requisitos Não-Funcionais (RNF)

### 10.2.1 Desempenho

| ID | Requisito | Critério de Aceitação |
|----|-----------|----------------------|
| RNF-01 | Tempo de resposta das APIs críticas | ≤ 2 segundos em 95% das requisições |
| RNF-02 | Latência da videochamada | ≤ 150ms em condições normais de rede |
| RNF-03 | Throughput mínimo | 500 requisições simultâneas por segundo |

### 10.2.2 Disponibilidade e Confiabilidade

| ID | Requisito | Critério de Aceitação |
|----|-----------|----------------------|
| RNF-04 | Disponibilidade do sistema | ≥ 99,5% (SLA) |
| RNF-05 | Tempo de recuperação após falha (RTO) | ≤ 4 horas |
| RNF-06 | Perda máxima de dados em falha (RPO) | ≤ 1 hora |
| RNF-07 | Backup automático de dados | Diário, com retenção de 30 dias |

### 10.2.3 Segurança

| ID | Requisito | Critério de Aceitação |
|----|-----------|----------------------|
| RNF-08 | Toda comunicação deve ser criptografada | TLS 1.2+ obrigatório em todos os endpoints |
| RNF-09 | Dados sensíveis devem ser criptografados em repouso | AES-256 para CPF e dados clínicos |
| RNF-10 | Conformidade com LGPD | Auditoria anual de conformidade aprovada |
| RNF-11 | Bloqueio após tentativas de login inválidas | Bloqueio após 5 tentativas consecutivas |

### 10.2.4 Escalabilidade e Manutenibilidade

| ID | Requisito | Critério de Aceitação |
|----|-----------|----------------------|
| RNF-12 | O sistema deve escalar horizontalmente | Auto-scaling configurado no Kubernetes |
| RNF-13 | Cada microsserviço deve ser implantável independentemente | Deploy sem impacto nos demais serviços |
| RNF-14 | Cobertura de testes | ≥ 80% de cobertura por microsserviço |

### 10.2.5 Usabilidade e Acessibilidade

| ID | Requisito | Critério de Aceitação |
|----|-----------|----------------------|
| RNF-15 | Interface responsiva para mobile e desktop | Testado nos principais navegadores e dispositivos |
| RNF-16 | Acessibilidade digital | Conformidade com WCAG 2.1 nível AA |

---

> **[TODO]** Revise e ajuste os critérios de aceitação conforme os requisitos reais do seu projeto.

---

*[← 09 – Casos de Uso](09-casos-uso.md) | [← Índice](README.md)*
