# 09 – Casos de Uso

## 9.1 Atores do Sistema

| Ator | Descrição |
|------|-----------|
| **Paciente** | Usuário que busca atendimento médico remoto |
| **Médico** | Profissional de saúde que realiza consultas |
| **Administrador** | Responsável pela gestão da plataforma |
| **Dispositivo IoT** | Wearable ou sensor que envia dados de saúde |
| **Sistema de Notificações** | Ator de sistema que dispara alertas e lembretes |

---

## 9.2 Lista de Casos de Uso

| ID | Caso de Uso | Ator Principal |
|----|-------------|----------------|
| UC-01 | Cadastrar Paciente | Paciente |
| UC-02 | Cadastrar Médico | Médico / Administrador |
| UC-03 | Realizar Login | Paciente / Médico / Administrador |
| UC-04 | Agendar Consulta | Paciente |
| UC-05 | Realizar Consulta por Vídeo | Paciente, Médico |
| UC-06 | Registrar Diagnóstico no Prontuário | Médico |
| UC-07 | Emitir Prescrição Digital | Médico |
| UC-08 | Visualizar Histórico Clínico | Paciente, Médico |
| UC-09 | Monitorar Sinais Vitais via IoT | Dispositivo IoT, Médico |
| UC-10 | Receber Notificação de Consulta | Paciente, Médico |
| UC-11 | Cancelar Consulta | Paciente, Médico |
| UC-12 | Exportar Dados Pessoais (LGPD) | Paciente |

---

## 9.3 Descrição Detalhada dos Casos de Uso Principais

### UC-04 – Agendar Consulta

**Ator Principal:** Paciente

**Pré-condições:**
- Paciente autenticado no sistema.
- Médico disponível no horário desejado.

**Fluxo Principal:**
1. Paciente acessa a tela de agendamento.
2. Sistema exibe lista de médicos disponíveis e especialidades.
3. Paciente seleciona médico e horário.
4. Sistema verifica disponibilidade em tempo real.
5. Paciente confirma o agendamento.
6. Sistema cria a consulta, gera sessão de vídeo e envia confirmação por e-mail/SMS.

**Fluxos Alternativos:**
- **4a.** Horário indisponível: sistema exibe outros horários disponíveis.
- **6a.** Falha no envio de notificação: sistema registra erro e reprocessa via fila.

**Pós-condições:**
- Consulta registrada com status `agendada`.
- Paciente e médico notificados.

---

### UC-05 – Realizar Consulta por Vídeo

**Ator Principal:** Paciente, Médico

**Pré-condições:**
- Consulta agendada e não cancelada.
- Ambos os usuários autenticados.
- Acesso à câmera e microfone concedido pelo navegador/app.

**Fluxo Principal:**
1. Paciente e médico acessam o link da consulta no horário agendado.
2. Sistema valida o token de acesso à sessão de vídeo.
3. Videochamada é iniciada entre paciente e médico.
4. Médico realiza anamnese e avaliação clínica.
5. Médico registra diagnóstico no prontuário (UC-06).
6. Médico emite prescrição digital, se necessário (UC-07).
7. Consulta é encerrada e status atualizado para `concluida`.

**Fluxos Alternativos:**
- **3a.** Queda de conexão: sistema mantém sessão ativa por 5 minutos aguardando reconexão.

**Pós-condições:**
- Consulta com status `concluida`.
- Prontuário atualizado com diagnóstico.
- Prescrição emitida (se aplicável).

---

### UC-09 – Monitorar Sinais Vitais via IoT

**Ator Principal:** Dispositivo IoT

**Pré-condições:**
- Dispositivo registrado e associado ao paciente.
- Paciente autenticado e com monitoramento ativo.

**Fluxo Principal:**
1. Dispositivo IoT coleta métrica (ex.: frequência cardíaca).
2. Dados são enviados ao broker MQTT via protocolo seguro (mTLS).
3. `iot-service` processa a métrica e armazena no banco de dados.
4. Sistema verifica se o valor está fora dos limites normais.
5. Se anômalo, `notification-service` alerta o médico responsável.

**Fluxos Alternativos:**
- **2a.** Falha na conexão: dispositivo armazena dados localmente e reenvia quando reconectado.

---

> **[TODO]** Adicione fluxos adicionais ou detalhe os demais casos de uso da sua lista.

---

*[← 08 – Implantação](08-implantacao.md) | [10 – Requisitos →](10-requisitos.md)*
