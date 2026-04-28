# 2.2 Estilo Arquitetural Escolhido

- **Estilo Principal:** Arquitetura Hexagonal (Ports and Adapters) com Microsserviços.
- **Justificativa e Trade-offs:** A escolha visa resolver o problema de acoplamento detectado na Fase 1, garantindo que as regras de negócio de telemedicina não dependam de frameworks ou bases de dados.

## Trade-offs

- **Isolamento do Domínio (Pró):** Garante a Integridade de Dados e facilita a manutenção, pois as mudanças na infraestrutura (ex: trocar a API de IA) não afetam o núcleo do sistema.
- **Testabilidade e Segurança (Pró):** Permite testar a lógica de negócio isoladamente através de mocks nas portas, essencial para a conformidade com LGPD/HIPAA.
- **Complexidade e Latência (Contra):** A separação em microsserviços e a abstração hexagonal aumentam a complexidade de implementação e podem introduzir uma pequena latência de rede entre componentes, o que exige uma monitorização rigorosa para manter a Disponibilidade.
