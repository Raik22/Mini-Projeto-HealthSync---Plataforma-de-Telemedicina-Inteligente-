# 01 – Introdução

## 1.1 Propósito

Este documento descreve a arquitetura de software da plataforma **HealthSync**, um sistema de telemedicina inteligente que conecta pacientes a profissionais de saúde de forma remota, segura e eficiente.

O objetivo deste documento é fornecer uma visão completa da estrutura técnica do sistema, orientando desenvolvedores, arquitetos e demais stakeholders durante o ciclo de vida do projeto.

## 1.2 Escopo

O **HealthSync** abrange as seguintes funcionalidades principais:

- Cadastro e autenticação de pacientes e médicos.
- Agendamento de consultas virtuais (videochamada).
- Prontuário eletrônico do paciente.
- Prescrição digital de medicamentos.
- Monitoramento remoto de sinais vitais via dispositivos IoT.
- Notificações e lembretes automáticos.

> **[TODO]** Descreva quaisquer funcionalidades adicionais específicas do seu escopo.

## 1.3 Definições, Siglas e Abreviações

| Termo | Definição |
|-------|-----------|
| API | Interface de Programação de Aplicações |
| IoT | Internet das Coisas |
| LGPD | Lei Geral de Proteção de Dados (Lei nº 13.709/2018) |
| REST | Representational State Transfer |
| JWT | JSON Web Token |
| SLA | Acordo de Nível de Serviço |
| EHR | Prontuário Eletrônico de Saúde (Electronic Health Record) |
| RNF | Requisito Não-Funcional |
| RF | Requisito Funcional |

## 1.4 Referências

- [Lei Geral de Proteção de Dados – LGPD](https://www.gov.br/cidadania/pt-br/acesso-a-informacao/lgpd)
- [Resolução CFM nº 2.314/2022 – Telemedicina](https://www.cfm.org.br/)
- [Padrão IEEE 1471 – Descrição de Arquitetura de Software]
- > **[TODO]** Adicione outras referências bibliográficas utilizadas no projeto.

## 1.5 Visão Geral do Documento

Este documento está estruturado conforme o **modelo Scaffolding**, dividido nas seguintes seções:

1. **Introdução** – contexto, escopo e terminologia.
2. **Visão Geral do Sistema** – objetivos e contexto de negócio.
3. **Arquitetura do Sistema** – estilo e decisões arquiteturais.
4. **Componentes e Módulos** – detalhamento dos módulos.
5. **Modelo de Dados** – estrutura e relacionamento dos dados.
6. **APIs e Interfaces** – contratos de comunicação.
7. **Segurança** – mecanismos de proteção e conformidade.
8. **Implantação** – estratégia de deploy e infraestrutura.
9. **Casos de Uso** – fluxos e atores principais.
10. **Requisitos** – funcionais e não-funcionais.

---

*[← Índice](README.md) | [02 – Visão Geral do Sistema →](02-visao-geral-sistema.md)*
