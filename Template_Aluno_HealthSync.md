Template do Aluno: Mini Projeto "HealthSync - Plataforma de Telemedicina Inteligente"
Aluno: Alan Raique Soares Nunes | Matrícula: 221059
Link do Repositório GitHub (Scaffolding): https://github.com/Raik22/Mini-Projeto-HealthSync---Plataforma-de-Telemedicina-Inteligente-

🟢 CICLO 1: Visão e Requisitos (Fase 1)
Preencher e entregar no AVA ao final do Ciclo 1.

1.1 Resumo do Cenário de Negócio
A HealthSync é uma plataforma de telemedicina que visa integrar consultas remotas, monitorização contínua via dispositivos wearables e diagnóstico auxiliado por Inteligência Artificial. O sistema resolve o desafio da fragmentação do cuidado médico, oferecendo um ecossistema centralizado para pacientes e profissionais de saúde. O contexto exige alta disponibilidade para atendimentos críticos e segurança rigorosa para o tratamento de dados sensíveis, garantindo que o histórico clínico esteja sempre acessível e protegido.

1.2 Atributos de Qualidade (RNFs) Priorizados
Segurança (LGPD/HIPAA): Essencial para proteger dados sensíveis de saúde e garantir conformidade legal, evitando fugas de informação.
Disponibilidade: O sistema deve estar operacional 24/7, pois falhas podem impedir o acesso médico em situações de urgência.
Escalabilidade: Necessária para processar o grande volume de dados provenientes de milhares de sensores IoT simultaneamente.
Integridade de Dados: Garante que as informações biométricas e recomendações da IA não sofram corrupção, assegurando diagnósticos precisos.
Interoperabilidade: Fundamental para a comunicação fluida entre diversos fabricantes de wearables e APIs externas de IA.

1.3 Diagrama de Contexto (C4 Nível 1)
[Descrever ou anexar o diagrama aqui.]

1.4 Classificação da Estratégia
Classificação: Balanceada.
Justificativa: A estratégia é balanceada pois utiliza tecnologias consolidadas para a persistência e segurança de dados (abordagem conservadora), enquanto adota microsserviços e integração com IA de ponta para inovação no monitoramento (abordagem ousada).

🔵 CICLO 2: Blueprint e Decisões (Fase 2)
Preencher e entregar no AVA ao final do Ciclo 2.

2.1 Diagrama de Containers (C4 Nível 2)
[Descrever ou anexar o diagrama aqui.]

2.2 Estilo Arquitetural Escolhido
Estilo Principal: Arquitetura Hexagonal (Ports and Adapters) com Microsserviços.
Justificativa e Trade-offs: A escolha visa resolver o problema de acoplamento detectado na Fase 1, garantindo que as regras de negócio de telemedicina não dependam de frameworks ou bases de dados.
Isolamento do Domínio (Pró): Garante a Integridade de Dados e facilita a manutenção, pois as mudanças na infraestrutura (ex: trocar a API de IA) não afetam o núcleo do sistema.
Testabilidade e Segurança (Pró): Permite testar a lógica de negócio isoladamente através de mocks nas portas, essencial para a conformidade com LGPD/HIPAA.
Complexidade e Latência (Contra): A separação em microsserviços e a abstração hexagonal aumentam a complexidade de implementação e podem introduzir uma pequena latência de rede entre componentes, o que exige uma monitorização rigorosa para manter a Disponibilidade.

2.3 Architecture Decision Record (ADR) Principal
Título: Adoção de Arquitetura Hexagonal para o Core da HealthSync
Status: Aceito
Contexto: A análise da Fase 1 revelou que o modelo N-Tier tradicional estava a gerar um acoplamento excessivo entre a lógica de negócio e os detalhes de persistência. Para um sistema de saúde que exige alta Interoperabilidade e escalabilidade para dados de sensores IoT, é vital que o domínio seja agnóstico a detalhes técnicos e frameworks (MARTIN, 2017).
Decisão:
Decidimos implementar o padrão de Portas e Adaptadores. O "Core" da aplicação conterá apenas as regras de negócio de telemedicina e monitorização. Toda a comunicação externa (Bases de Dados, API de IA, Wearables) será feita através de interfaces definidas pelo domínio (Ports) e implementadas pela infraestrutura (Adapters).
Justificativa:
Redução da Dívida Técnica: Evita que a lógica médica fique "presa" a tecnologias específicas (ex: um banco SQL ou uma biblioteca de IA específica).
Evolução Facilitada: Permite substituir fornecedores de wearables ou modelos de IA sem reescrever o motor de regras de diagnóstico.
Conformidade Técnica: Alinha o projeto com a Regra de Dependência (Dependency Rule), onde o domínio não conhece a infraestrutura, mitigando os riscos de falhas sistêmicas apontados na revisão do Ciclo 1.

🔴 CICLO 3: Cloud e Resiliência (Fase 3)
Preencher e entregar no AVA ao final do Ciclo 3.

3.1 Estratégia de Cloud e Implantação
[Descreva como sua arquitetura será implantada em um ambiente de nuvem (ex: AWS, Azure, GCP). Qual o modelo de serviço (IaaS, PaaS, Serverless)? Como o sistema será escalado e monitorado?]

3.2 Análise de Fragilidade e Mitigação
Ponto Frágil: [Identifique a maior fraqueza ou risco da sua arquitetura em um cenário de produção (ex: falha de um serviço crítico, pico de tráfego inesperado, vulnerabilidade de segurança).]
Mitigação: [Como você minimizaria esse risco? Quais estratégias de resiliência (ex: circuit breaker, retry, fallback, multi-região) seriam aplicadas?]

3.3 Parecer Técnico Final
[Resumo executivo (até 10 linhas) defendendo por que sua arquitetura é a melhor escolha para o cliente, considerando os requisitos de negócio, os RNFs e a estratégia de implantação. Qual o valor agregado da sua solução?]

🏆 BÔNUS: Evolução Arquitetural (Gamificação)
Opcional - Preencher apenas se houver melhoria estrutural documentada no GitHub.

[Descreva brevemente a melhoria arquitetural que você implementou no seu repositório GitHub para fins de bônus de nota. Referencie a nova ADR e o diagrama atualizado (se houver) no GitHub. Ex: Migração de um componente para Serverless, implementação de um padrão de resiliência, otimização de custo em cloud. Lembre-se: a melhoria deve ser arquitetural, não apenas textual.]

SURPREENDA-ME! :D

📚 Referências Bibliográficas
Pressman, R. S. (2021). Engenharia de Software: Uma Abordagem Profissional. McGraw Hill. (Capítulos selecionados conforme o tema da aula).
Richards, M., & Ford, N. (2020). Fundamentals of Software Architecture: An Engineering Approach. O'Reilly Media.
Martin, R. C. (2017). Clean Architecture: A Craftsman's Guide to Software Structure and Design. Prentice Hall.
C4 Model for Software Architecture. (s.d.). Disponível em: https://c4model.com/
Architecture Decision Records (ADRs). (s.d.). Disponível em: https://adr.github.io/
