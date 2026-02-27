# 02 – Visão Geral do Sistema

## 2.1 Objetivos do Sistema

O **HealthSync** tem como objetivo principal democratizar o acesso à saúde por meio da tecnologia, permitindo que pacientes realizem consultas médicas remotamente, com qualidade, segurança e conformidade regulatória.

**Objetivos específicos:**

- Reduzir o tempo de espera para consultas médicas.
- Disponibilizar atendimento médico em regiões com baixa cobertura de saúde.
- Centralizar o histórico de saúde do paciente em um prontuário digital unificado.
- Permitir o monitoramento contínuo de pacientes crônicos via dispositivos IoT.

## 2.2 Contexto do Sistema

```
+-------------------+          +---------------------+
|    Paciente       |  <---->  |                     |
+-------------------+          |     HealthSync      |
                               |   (Telemedicina)    |
+-------------------+          |                     |
|    Médico/        |  <---->  |                     |
|    Especialista   |          +----------+----------+
+-------------------+                     |
                                          |
+-------------------+          +----------v----------+
|  Dispositivos     |  <---->  |  Serviços Externos  |
|  IoT / Wearables  |          |  (Labs, Farmácias,  |
+-------------------+          |   Planos de Saúde)  |
                               +---------------------+
```

> **[TODO]** Substitua o diagrama ASCII pelo diagrama de contexto real do projeto (ex.: diagrama C4 nível 1).

## 2.3 Usuários e Partes Interessadas

| Usuário / Stakeholder | Papel | Necessidades Principais |
|-----------------------|-------|-------------------------|
| Paciente | Usuário final | Agendar consultas, acessar prontuário, receber prescrições |
| Médico / Especialista | Usuário final | Realizar consultas, prescrever, consultar histórico |
| Administrador do Sistema | Operador | Gerenciar usuários, monitorar plataforma |
| Equipe de TI / DevOps | Técnico | Manter infraestrutura e disponibilidade |
| Planos de Saúde | Parceiro externo | Integração de cobertura e faturamento |
| Laboratórios | Parceiro externo | Envio de resultados de exames |

## 2.4 Restrições do Sistema

- O sistema deve estar em conformidade com a **LGPD** (Lei nº 13.709/2018).
- Dados de saúde devem ser armazenados em território nacional (conforme LGPD).
- O sistema deve seguir as diretrizes do **CFM** para telemedicina.
- Disponibilidade mínima de **99,5%** (SLA).
- Tempo de resposta máximo de **2 segundos** para operações críticas.

> **[TODO]** Adicione restrições técnicas ou regulatórias específicas do seu contexto.

## 2.5 Premissas

- Os usuários possuem acesso à internet com banda suficiente para videochamadas.
- Os dispositivos IoT seguem o protocolo MQTT para envio de dados.
- Os médicos são previamente cadastrados e verificados pelo CRM.

---

*[← 01 – Introdução](01-introducao.md) | [03 – Arquitetura do Sistema →](03-arquitetura-sistema.md)*
