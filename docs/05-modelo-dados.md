# 05 – Modelo de Dados

## 5.1 Entidades Principais

### 5.1.1 Paciente (Patient)

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `id` | UUID | Identificador único |
| `nome` | VARCHAR(150) | Nome completo |
| `cpf` | CHAR(11) | CPF (criptografado) |
| `data_nascimento` | DATE | Data de nascimento |
| `email` | VARCHAR(200) | E-mail de contato |
| `telefone` | VARCHAR(20) | Número de telefone |
| `endereco` | JSONB | Endereço completo |
| `plano_saude_id` | UUID | Referência ao plano de saúde |
| `criado_em` | TIMESTAMP | Data de criação do registro |
| `atualizado_em` | TIMESTAMP | Data da última atualização |

---

### 5.1.2 Médico (Doctor)

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `id` | UUID | Identificador único |
| `nome` | VARCHAR(150) | Nome completo |
| `crm` | VARCHAR(20) | Número do CRM |
| `especialidade` | VARCHAR(100) | Especialidade médica |
| `email` | VARCHAR(200) | E-mail profissional |
| `telefone` | VARCHAR(20) | Contato profissional |
| `disponibilidade` | JSONB | Grade de horários disponíveis |
| `criado_em` | TIMESTAMP | Data de criação do registro |

---

### 5.1.3 Consulta (Appointment)

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `id` | UUID | Identificador único |
| `paciente_id` | UUID | Referência ao paciente |
| `medico_id` | UUID | Referência ao médico |
| `data_hora` | TIMESTAMP | Data e hora da consulta |
| `duracao_min` | INTEGER | Duração em minutos |
| `status` | ENUM | `agendada`, `em_andamento`, `concluida`, `cancelada` |
| `video_session_id` | VARCHAR | ID da sessão de vídeo |
| `notas` | TEXT | Observações da consulta |
| `criado_em` | TIMESTAMP | Data de criação |

---

### 5.1.4 Prontuário / Registro Clínico (EHR Record)

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `id` | UUID | Identificador único |
| `paciente_id` | UUID | Referência ao paciente |
| `consulta_id` | UUID | Referência à consulta (opcional) |
| `tipo` | ENUM | `diagnostico`, `exame`, `alergia`, `medicacao`, `observacao` |
| `descricao` | TEXT | Descrição clínica |
| `dados` | JSON | Dados estruturados variáveis por tipo |
| `criado_por` | UUID | Médico responsável |
| `criado_em` | TIMESTAMP | Data do registro |

---

### 5.1.5 Prescrição (Prescription)

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `id` | UUID | Identificador único |
| `consulta_id` | UUID | Referência à consulta |
| `paciente_id` | UUID | Referência ao paciente |
| `medico_id` | UUID | Referência ao médico |
| `medicamentos` | JSONB | Lista de medicamentos, doses e posologia |
| `assinatura_digital` | TEXT | Hash da assinatura digital |
| `validade` | DATE | Data de validade da prescrição |
| `criado_em` | TIMESTAMP | Data de emissão |

---

### 5.1.6 Métrica IoT (IoT Metric)

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `id` | UUID | Identificador único |
| `paciente_id` | UUID | Referência ao paciente |
| `dispositivo_id` | VARCHAR(100) | Identificador do dispositivo |
| `tipo_metrica` | ENUM | `freq_cardiaca`, `pressao_arterial`, `glicemia`, `spo2` |
| `valor` | FLOAT | Valor medido |
| `unidade` | VARCHAR(20) | Unidade de medida (ex.: bpm, mmHg) |
| `coletado_em` | TIMESTAMP | Momento da coleta |

---

## 5.2 Diagrama Entidade-Relacionamento (ER)

```
+-------------+       +-----------------+       +----------+
|   Patient   |------>|   Appointment   |<------|  Doctor  |
|-------------|  1:N  |-----------------|  1:N  |----------|
| id (PK)     |       | id (PK)         |       | id (PK)  |
| nome        |       | paciente_id(FK) |       | nome     |
| cpf         |       | medico_id (FK)  |       | crm      |
| email       |       | data_hora       |       | especial.|
+-------------+       | status          |       +----------+
      |               +-----------------+
      |  1:N                 | 1:1
      v                      v
+-------------+       +-----------------+
| IoT Metric  |       |  Prescription   |
|-------------|       |-----------------|
| id (PK)     |       | id (PK)         |
| paciente_id |       | consulta_id(FK) |
| tipo_metrica|       | paciente_id(FK) |
| valor       |       | medicamentos    |
+-------------+       +-----------------+
      |                      | 1:N
      |               +------v----------+
      |               |   EHR Record   |
      |               |----------------|
      |               | id (PK)        |
      +-------------->| paciente_id(FK)|
                      | tipo           |
                      | descricao      |
                      +----------------+
```

> **[TODO]** Substitua o diagrama ASCII pelo diagrama ER formal (ex.: gerado com dbdiagram.io, draw.io ou equivalente).

---

*[← 04 – Componentes e Módulos](04-componentes.md) | [06 – APIs e Interfaces →](06-apis.md)*
