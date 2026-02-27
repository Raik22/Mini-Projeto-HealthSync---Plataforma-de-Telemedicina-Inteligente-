# 06 – APIs e Interfaces

## 6.1 Convenções da API

- **Protocolo:** HTTPS (TLS 1.2+)
- **Formato:** JSON (`Content-Type: application/json`)
- **Autenticação:** Bearer Token (JWT) no header `Authorization`
- **Versionamento:** Prefixo `/api/v1/` em todos os endpoints
- **Paginação:** Parâmetros `page` (número da página) e `limit` (itens por página)
- **Códigos de Status HTTP:** conforme RFC 7231

### Códigos de Status Utilizados

| Código | Significado |
|--------|-------------|
| `200 OK` | Requisição bem-sucedida |
| `201 Created` | Recurso criado com sucesso |
| `204 No Content` | Requisição bem-sucedida sem corpo de resposta |
| `400 Bad Request` | Dados de entrada inválidos |
| `401 Unauthorized` | Token ausente ou inválido |
| `403 Forbidden` | Acesso não autorizado ao recurso |
| `404 Not Found` | Recurso não encontrado |
| `409 Conflict` | Conflito de dados (ex.: CPF duplicado) |
| `500 Internal Server Error` | Erro interno do servidor |

---

## 6.2 Autenticação

### POST `/api/v1/auth/login`

Autentica o usuário e retorna tokens de acesso.

**Request:**
```json
{
  "email": "paciente@email.com",
  "senha": "SenhaSegura@123"
}
```

**Response `200 OK`:**
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIs...",
  "refresh_token": "dGhpcyBpcyBhIHJlZnJlc2...",
  "expires_in": 3600,
  "token_type": "Bearer"
}
```

---

## 6.3 Consultas (Appointments)

### POST `/api/v1/appointments`

Agenda uma nova consulta.

**Request:**
```json
{
  "paciente_id": "uuid-paciente",
  "medico_id": "uuid-medico",
  "data_hora": "2025-06-15T14:00:00Z",
  "duracao_min": 30
}
```

**Response `201 Created`:**
```json
{
  "id": "uuid-consulta",
  "status": "agendada",
  "video_session_id": "session-abc123",
  "data_hora": "2025-06-15T14:00:00Z"
}
```

---

### GET `/api/v1/appointments/{id}`

Retorna os detalhes de uma consulta.

**Response `200 OK`:**
```json
{
  "id": "uuid-consulta",
  "paciente": { "id": "uuid-paciente", "nome": "João Silva" },
  "medico": { "id": "uuid-medico", "nome": "Dra. Ana Lima", "especialidade": "Clínica Geral" },
  "data_hora": "2025-06-15T14:00:00Z",
  "duracao_min": 30,
  "status": "agendada"
}
```

---

## 6.4 Prontuário Eletrônico (EHR)

### POST `/api/v1/ehr/{patientId}/records`

Adiciona um registro clínico ao prontuário do paciente.

**Request:**
```json
{
  "consulta_id": "uuid-consulta",
  "tipo": "diagnostico",
  "descricao": "Hipertensão arterial leve (CID: I10)",
  "dados": {
    "cid": "I10",
    "gravidade": "leve"
  }
}
```

**Response `201 Created`:**
```json
{
  "id": "uuid-registro",
  "paciente_id": "uuid-paciente",
  "tipo": "diagnostico",
  "criado_em": "2025-06-15T14:45:00Z"
}
```

---

## 6.5 Prescrição Digital

### POST `/api/v1/prescriptions`

Emite uma prescrição digital assinada.

**Request:**
```json
{
  "consulta_id": "uuid-consulta",
  "paciente_id": "uuid-paciente",
  "medicamentos": [
    {
      "nome": "Losartana Potássica",
      "dose": "50mg",
      "posologia": "1 comprimido ao dia pela manhã",
      "duracao_dias": 30
    }
  ]
}
```

**Response `201 Created`:**
```json
{
  "id": "uuid-prescricao",
  "assinatura_digital": "sha256:abc123...",
  "validade": "2025-07-15",
  "pdf_url": "https://storage.healthsync.com/prescricoes/uuid-prescricao.pdf"
}
```

---

> **[TODO]** Documente os demais endpoints relevantes para o seu projeto (IoT, notificações, etc.).

---

*[← 05 – Modelo de Dados](05-modelo-dados.md) | [07 – Segurança →](07-seguranca.md)*
