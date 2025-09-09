# Relatório Técnico: Sistema de Agendamento de Consultas Médicas

## 1. Introdução

Este relatório técnico detalha as etapas iniciais de análise e design para o desenvolvimento de um sistema web de agendamento de consultas médicas. O projeto surge da necessidade de modernizar e otimizar o processo de agendamento atualmente manual e baseado em papel de uma empresa de médio porte. O método atual tem demonstrado ineficiências significativas, incluindo a duplicação de horários, a perda de registros importantes e uma comunicação deficiente entre médicos, recepcionistas e pacientes. Tais problemas não apenas comprometem a eficiência operacional, mas também afetam a qualidade do serviço prestado e a satisfação dos usuários.

A análise de requisitos é uma fase crítica no ciclo de vida do desenvolvimento de software, servindo como a ponte entre as necessidades do negócio e a solução tecnológica. Uma compreensão clara e abrangente dos requisitos é fundamental para garantir que o sistema desenvolvido atenda às expectativas dos stakeholders, minimize retrabalhos e entregue valor real. Este documento aborda o levantamento, a análise e a modelagem inicial dos requisitos do sistema, estabelecendo uma base sólida para as fases subsequentes de implementação e testes. A modelagem do sistema, por sua vez, transforma os requisitos abstratos em representações visuais e textuais, facilitando a comunicação e a validação com todas as partes interessadas e fornecendo um blueprint para a arquitetura do software.



## 2. Levantamento de Requisitos

O levantamento de requisitos é a primeira etapa para compreender as necessidades do sistema. Nesta fase, foram identificados os requisitos funcionais e não funcionais, suas prioridades e as necessidades específicas de cada tipo de usuário.

### 2.1. Requisitos Funcionais

Os requisitos funcionais descrevem as funcionalidades que o sistema deve oferecer para atender às necessidades dos usuários e do negócio. A seguir, uma lista dos requisitos funcionais identificados:

- Agendamento de consultas médicas (paciente, médico, recepcionista)
- Visualização de horários disponíveis (paciente, médico, recepcionista)
- Cancelamento de consultas (paciente, médico, recepcionista)
- Edição de agendamentos (recepcionista)
- Cadastro de pacientes (recepcionista)
- Cadastro de médicos (recepcionista)
- Gerenciamento de especialidades médicas (recepcionista)
- Geração de relatórios de agendamento (recepcionista)
- Notificações de agendamento (paciente, médico)
- Busca por agendamentos (recepcionista, médico, paciente)
- Autenticação de usuários (paciente, médico, recepcionista)

### 2.2. Requisitos Não Funcionais

Os requisitos não funcionais especificam critérios que podem ser usados para julgar a operação de um sistema, em vez de comportamentos específicos. Eles são cruciais para a qualidade e a experiência do usuário. Os requisitos não funcionais identificados são:

- **Desempenho:** O sistema deve ser capaz de lidar com um grande volume de agendamentos simultâneos sem degradação perceptível de desempenho.
- **Segurança:** O sistema deve garantir a confidencialidade e integridade dos dados dos pacientes e médicos, com controle de acesso baseado em perfis de usuário.
- **Usabilidade:** A interface do usuário deve ser intuitiva e fácil de usar para todos os tipos de usuários (pacientes, médicos e recepcionistas).
- **Disponibilidade:** O sistema deve estar disponível 24 horas por dia, 7 dias por semana, com tempo de inatividade mínimo.
- **Confiabilidade:** O sistema deve ser robusto e tolerante a falhas, garantindo que os dados não sejam perdidos em caso de problemas.
- **Escalabilidade:** O sistema deve ser capaz de escalar para suportar um aumento futuro no número de usuários e agendamentos.
- **Manutenibilidade:** O código do sistema deve ser bem documentado e fácil de manter e modificar.
- **Portabilidade:** O sistema deve ser compatível com diferentes navegadores web e dispositivos (desktop, tablet, mobile).
- **Integridade de Dados:** O sistema deve garantir a consistência e precisão dos dados, evitando duplicidade de horários e perda de registros.


### 2.3. Necessidades dos Usuários

A compreensão das necessidades de cada perfil de usuário é fundamental para o desenvolvimento de um sistema centrado no usuário. As principais necessidades identificadas são:

**Paciente:**
- Agendar consultas de forma rápida e fácil, sem burocracia.
- Visualizar seus agendamentos futuros e passados.
- Cancelar consultas quando necessário.
- Receber notificações sobre seus agendamentos (confirmação, lembretes).
- Buscar por médicos e especialidades.

**Médico:**
- Visualizar sua agenda de consultas de forma clara e organizada.
- Confirmar e cancelar consultas de seus pacientes.
- Acessar informações básicas dos pacientes agendados.
- Receber notificações sobre novos agendamentos ou cancelamentos.

**Recepcionista:**
- Gerenciar agendamentos de todos os médicos e pacientes.
- Cadastrar novos pacientes e médicos.
- Editar e cancelar agendamentos.
- Buscar por agendamentos específicos.
- Gerenciar horários de atendimento dos médicos.
- Gerar relatórios de agendamento para a gestão.
- Ter uma visão geral da disponibilidade dos médicos.



## 3. Análise de Requisitos

A fase de análise de requisitos visa refinar, organizar e validar os requisitos levantados, além de identificar e resolver possíveis conflitos e inconsistências. Esta etapa é crucial para garantir que o sistema a ser desenvolvido seja coeso e atenda de forma eficaz às necessidades do negócio.

### 3.1. Organização e Validação dos Requisitos

Os requisitos foram organizados e validados para garantir clareza, completude e consistência. A validação foi realizada considerando as necessidades dos stakeholders (pacientes, médicos e recepcionistas) e as restrições do sistema. Os requisitos funcionais e não funcionais essenciais (Must-have) foram priorizados para a primeira versão do sistema, conforme detalhado na seção de Levantamento de Requisitos.

### 3.2. Conflitos e Inconsistências Identificados e Soluções Propostas

Durante a análise, foram identificados potenciais conflitos e inconsistências, principalmente relacionados à gestão de agendamentos e permissões de usuários. As soluções propostas visam mitigar esses riscos e garantir a robustez do sistema.

#### Conflito 1: Duplicidade de Agendamentos
- **Descrição:** O processo manual atual sofre com a duplicidade de horários. No sistema, isso poderia ocorrer se múltiplos usuários tentassem agendar o mesmo horário simultaneamente ou se houvesse falha na validação.
- **Solução Proposta:** Implementar um mecanismo de validação em tempo real que verifique a disponibilidade do horário antes de confirmar o agendamento. Utilizar transações de banco de dados para garantir a atomicidade da operação de agendamento, prevenindo condições de corrida.

#### Conflito 2: Perda de Registros
- **Descrição:** A perda de registros é um problema no processo manual. No sistema, isso poderia acontecer devido a falhas no armazenamento de dados ou erros na manipulação de informações.
- **Solução Proposta:** Implementar um sistema robusto de persistência de dados com backups regulares e redundância. Adotar validações de entrada de dados para garantir que informações críticas sejam sempre salvas corretamente. Utilizar logs de auditoria para rastrear todas as operações de criação, edição e exclusão de agendamentos.

#### Conflito 3: Conflito de Permissões para Edição/Cancelamento
- **Descrição:** Pacientes, médicos e recepcionistas podem querer editar ou cancelar agendamentos. É necessário definir claramente quem tem permissão para fazer o quê para evitar ações não autorizadas ou sobreposições.
- **Solução Proposta:** Definir uma matriz de permissões clara:
    - **Paciente:** Pode agendar e cancelar *suas próprias* consultas.
    - **Médico:** Pode visualizar *sua própria* agenda, confirmar e cancelar consultas *em sua própria agenda*.
    - **Recepcionista:** Tem permissão total para agendar, editar e cancelar *qualquer* consulta, além de gerenciar cadastros de pacientes e médicos.
    - Implementar controle de acesso baseado em papéis (RBAC) para aplicar essas permissões no sistema.

#### Conflito 4: Comunicação Ineficiente (Requisito Não Funcional vs. Funcional)
- **Descrição:** A falta de comunicação é um problema atual. Embora o requisito de 'Notificações de agendamento' seja funcional, ele aborda diretamente o problema não funcional de comunicação ineficiente.
- **Solução Proposta:** Priorizar a implementação de notificações automáticas (e-mail, SMS) para pacientes e médicos sobre agendamentos, alterações e cancelamentos. Isso transformará um problema de comunicação em uma solução funcional e automatizada.

### 3.3. Critérios de Aceitação

Os critérios de aceitação definem as condições que o sistema deve satisfazer para ser considerado aceitável pelos stakeholders. Eles são baseados nos requisitos priorizados e nas soluções propostas para os conflitos.

#### Critérios de Aceitação para Requisitos Funcionais Essenciais:

1.  **Agendamento de Consultas:**
    *   **CA1.1:** O sistema deve permitir que um paciente agende uma consulta selecionando um médico, especialidade, data e horário disponíveis.
    *   **CA1.2:** O sistema deve permitir que um médico visualize e confirme um agendamento feito por um paciente.
    *   **CA1.3:** O sistema deve permitir que uma recepcionista agende uma consulta para um paciente, selecionando médico, especialidade, data e horário, e associando-a a um paciente existente ou cadastrando um novo.
    *   **CA1.4:** O sistema deve impedir o agendamento de horários já ocupados ou fora do horário de atendimento do médico.

2.  **Visualização de Horários:**
    *   **CA2.1:** O paciente deve conseguir visualizar os horários disponíveis de um médico para uma determinada especialidade e data.
    *   **CA2.2:** O médico deve conseguir visualizar sua agenda completa, com detalhes das consultas agendadas (paciente, horário, especialidade).
    *   **CA2.3:** A recepcionista deve conseguir visualizar a agenda de qualquer médico, com detalhes das consultas agendadas.

3.  **Cancelamento de Consultas:**
    *   **CA3.1:** O paciente deve conseguir cancelar uma consulta agendada por ele mesmo, desde que dentro do prazo estabelecido (ex: 24h antes).
    *   **CA3.2:** O médico deve conseguir cancelar uma consulta em sua agenda, com notificação ao paciente.
    *   **CA3.3:** A recepcionista deve conseguir cancelar qualquer consulta, com notificação ao paciente e médico.

4.  **Cadastro de Pacientes:**
    *   **CA4.1:** A recepcionista deve conseguir cadastrar um novo paciente, informando nome completo, CPF, data de nascimento, telefone e e-mail.
    *   **CA4.2:** O sistema deve validar os dados de entrada do paciente (ex: formato de e-mail, CPF único).

5.  **Autenticação de Usuários:**
    *   **CA5.1:** O sistema deve permitir que pacientes, médicos e recepcionistas façam login com credenciais válidas (usuário e senha).
    *   **CA5.2:** O sistema deve direcionar o usuário para a interface correspondente ao seu perfil após o login bem-sucedido.
    *   **CA5.3:** O sistema deve exibir uma mensagem de erro clara para credenciais inválidas.

#### Critérios de Aceitação para Requisitos Não Funcionais Essenciais:

1.  **Segurança:**
    *   **CA6.1:** O sistema deve utilizar criptografia para senhas de usuários.
    *   **CA6.2:** O acesso a funcionalidades sensíveis (ex: edição de dados de pacientes) deve ser restrito por perfil de usuário.
    *   **CA6.3:** O sistema deve registrar tentativas de login falhas.

2.  **Usabilidade:**
    *   **CA7.1:** A interface de agendamento deve ser navegável em no máximo 3 cliques para um agendamento simples.
    *   **CA7.2:** As mensagens de erro e sucesso devem ser claras e informativas.
    *   **CA7.3:** O layout deve ser responsivo, adaptando-se a diferentes tamanhos de tela (desktop, tablet, mobile).

3.  **Integridade de Dados:**
    *   **CA8.1:** O sistema deve impedir a criação de dois agendamentos para o mesmo médico, no mesmo horário e data.
    *   **CA8.2:** Todas as operações de agendamento (criação, edição, cancelamento) devem ser atômicas, garantindo que sejam totalmente concluídas ou totalmente revertidas.
    *   **CA8.3:** O sistema deve notificar o usuário em caso de falha na persistência de dados.



## 4. Modelagem de Sistemas

A modelagem do sistema é uma etapa crucial para visualizar a arquitetura e o comportamento do software antes da implementação. Utilizando a Linguagem de Modelagem Unificada (UML), foram elaborados diagramas de Caso de Uso, de Classes e de Sequência, que fornecem diferentes perspectivas sobre o sistema.

### 4.1. Diagrama de Casos de Uso

O Diagrama de Casos de Uso representa a funcionalidade do sistema do ponto de vista do usuário, mostrando os atores (usuários ou outros sistemas que interagem com o sistema) e os casos de uso (funções que o sistema executa). Ele é fundamental para entender o escopo do sistema e como os diferentes usuários interagem com ele.

![Diagrama de Casos de Uso](https://private-us-east-1.manuscdn.com/sessionFile/pzZIAnZrjqX8BFcUID9SYs/sandbox/aqDI53yOy4zkekYVY5HdsS-images_1757424804524_na1fn_L2hvbWUvdWJ1bnR1L3VzZV9jYXNlX2RpYWdyYW0.png?Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9wcml2YXRlLXVzLWVhc3QtMS5tYW51c2Nkbi5jb20vc2Vzc2lvbkZpbGUvcHpaSUFuWnJqcVg4QkZjVUlEOVNZcy9zYW5kYm94L2FxREk1M3lPeTR6a2VrWVZZNUhkc1MtaW1hZ2VzXzE3NTc0MjQ4MDQ1MjRfbmExZm5fTDJodmJXVXZkV0oxYm5SMUwzVnpaVjlqWVhObFgyUnBZV2R5WVcwLnBuZyIsIkNvbmRpdGlvbiI6eyJEYXRlTGVzc1RoYW4iOnsiQVdTOkVwb2NoVGltZSI6MTc5ODc2MTYwMH19fV19&Key-Pair-Id=K2HSFNDJXOU9YS&Signature=mtIgJrt31muEv6sU~dS~mJwhBrO6OH44EqDv3PTshtf8OkKWM5DL74Bfe1tebSyUfSkfoeK3-W-NGL9eszjhMuatIIhyepquAvlwPUv969lAot7YjapJ8LfqmRW-pX7srTzSvQr7aJOCSMkse2FVCKMHTjlGzcX4492wztVd~LSDm~8IAhKghuo~iypo6iwWIcIUPAmw2iactoR2UmymSG1zUtOeBLfgTtpR1weTaOtYhvFSrAy6u7dJJXqgrvwgpkbw49KFFL8QJW5yCuj6nWdR1NU4NPTNgGoqUxUhja5EjlnJ9oF2A5fAU9XP4EqIh9EkpEUqhQku6e8Fb07qoA__)

#### Descrição dos Casos de Uso

As descrições textuais detalham o fluxo de eventos para cada caso de uso, incluindo pré-condições, pós-condições, fluxos principais e alternativos. Isso garante uma compreensão aprofundada do comportamento esperado do sistema para cada funcionalidade.

**UC1: Agendar Consulta**
- **Ator Principal:** Paciente, Recepcionista
- **Objetivo:** Permitir que um usuário agende uma nova consulta médica.
- **Pré-condições:** O usuário deve estar autenticado no sistema. Deve haver médicos e horários disponíveis.
- **Fluxo Principal:**
    1. O usuário seleciona a opção de agendar consulta.
    2. O sistema exibe os campos para seleção de médico, especialidade, data e horário.
    3. O usuário preenche os dados e confirma o agendamento.
    4. O sistema verifica a disponibilidade do horário.
    5. Se disponível, o sistema registra o agendamento e envia uma confirmação ao paciente e médico.
- **Pós-condições:** Uma nova consulta é registrada no sistema. O paciente e o médico recebem uma notificação.
- **Fluxos Alternativos:**
    - **4a. Horário Indisponível:** Se o horário selecionado não estiver disponível, o sistema informa o usuário e permite que ele escolha outro horário.
    - **5a. Falha no Registro:** Se houver falha ao registrar o agendamento, o sistema informa o usuário e não persiste a consulta.

**UC2: Visualizar Horários Disponíveis**
- **Ator Principal:** Paciente, Recepcionista
- **Objetivo:** Permitir que um usuário visualize os horários que estão abertos para agendamento.
- **Pré-condições:** O usuário deve estar autenticado.
- **Fluxo Principal:**
    1. O usuário seleciona a opção de visualizar horários disponíveis.
    2. O sistema solicita critérios de busca (ex: médico, especialidade, data).
    3. O usuário informa os critérios.
    4. O sistema exibe uma lista de horários disponíveis que correspondem aos critérios.
- **Pós-condições:** O usuário visualiza os horários disponíveis.

**UC3: Visualizar Agenda**
- **Ator Principal:** Médico, Recepcionista
- **Objetivo:** Permitir que um médico ou recepcionista visualize a agenda de consultas.
- **Pré-condições:** O usuário deve estar autenticado.
- **Fluxo Principal:**
    1. O usuário seleciona a opção de visualizar agenda.
    2. O sistema exibe a agenda de consultas para o médico logado ou permite que a recepcionista selecione um médico para visualizar a agenda.
    3. A agenda é exibida com detalhes das consultas (paciente, horário, especialidade).
- **Pós-condições:** O usuário visualiza a agenda de consultas.

**UC4: Cancelar Consulta**
- **Ator Principal:** Paciente, Médico, Recepcionista
- **Objetivo:** Permitir que um usuário cancele uma consulta agendada.
- **Pré-condições:** O usuário deve estar autenticado. A consulta deve existir e ser passível de cancelamento (ex: dentro do prazo).
- **Fluxo Principal:**
    1. O usuário seleciona a consulta que deseja cancelar.
    2. O sistema solicita confirmação do cancelamento.
    3. O usuário confirma.
    4. O sistema marca a consulta como cancelada e notifica as partes envolvidas.
- **Pós-condições:** A consulta é marcada como cancelada. Paciente e médico são notificados.

**UC5: Cadastrar Paciente**
- **Ator Principal:** Recepcionista
- **Objetivo:** Permitir que a recepcionista cadastre um novo paciente no sistema.
- **Pré-condições:** A recepcionista deve estar autenticada.
- **Fluxo Principal:**
    1. A recepcionista seleciona a opção de cadastrar paciente.
    2. O sistema exibe o formulário de cadastro de paciente.
    3. A recepcionista preenche os dados do paciente (nome, CPF, telefone, e-mail, etc.) e salva.
    4. O sistema valida os dados e registra o novo paciente.
- **Pós-condições:** Um novo paciente é registrado no sistema.

**UC6: Autenticar Usuário**
- **Ator Principal:** Paciente, Médico, Recepcionista
- **Objetivo:** Permitir que um usuário acesse o sistema com suas credenciais.
- **Pré-condições:** O usuário deve ter um cadastro no sistema.
- **Fluxo Principal:**
    1. O usuário acessa a página de login.
    2. O usuário insere seu nome de usuário e senha.
    3. O sistema valida as credenciais.
    4. Se as credenciais forem válidas, o sistema concede acesso ao usuário e o redireciona para a página inicial de seu perfil.
- **Pós-condições:** O usuário está logado no sistema.
- **Fluxos Alternativos:**
    - **3a. Credenciais Inválidas:** Se as credenciais forem inválidas, o sistema exibe uma mensagem de erro e permite que o usuário tente novamente.

**UC7: Editar Agendamento**
- **Ator Principal:** Recepcionista
- **Objetivo:** Permitir que a recepcionista edite os detalhes de um agendamento existente.
- **Pré-condições:** A recepcionista deve estar autenticada. O agendamento deve existir.
- **Fluxo Principal:**
    1. A recepcionista busca e seleciona o agendamento a ser editado.
    2. O sistema exibe os detalhes do agendamento em um formulário editável.
    3. A recepcionista faz as alterações necessárias (ex: horário, médico).
    4. O sistema valida as alterações e atualiza o agendamento.
    5. O sistema notifica o paciente e o médico sobre a alteração.
- **Pós-condições:** O agendamento é atualizado no sistema. Paciente e médico são notificados.

**UC8: Cadastrar Médico**
- **Ator Principal:** Recepcionista
- **Objetivo:** Permitir que a recepcionista cadastre um novo médico no sistema.
- **Pré-condições:** A recepcionista deve estar autenticada.
- **Fluxo Principal:**
    1. A recepcionista seleciona a opção de cadastrar médico.
    2. O sistema exibe o formulário de cadastro de médico.
    3. A recepcionista preenche os dados do médico (nome, CRM, especialidade, horários de atendimento, etc.) e salva.
    4. O sistema valida os dados e registra o novo médico.
- **Pós-condições:** Um novo médico é registrado no sistema.

**UC9: Buscar Agendamento**
- **Ator Principal:** Paciente, Médico, Recepcionista
- **Objetivo:** Permitir que um usuário busque por agendamentos específicos.
- **Pré-condições:** O usuário deve estar autenticado.
- **Fluxo Principal:**
    1. O usuário seleciona a opção de buscar agendamento.
    2. O sistema solicita critérios de busca (ex: nome do paciente, data, médico).
    3. O usuário informa os critérios.
    4. O sistema exibe uma lista de agendamentos que correspondem aos critérios.
- **Pós-condições:** O usuário visualiza os agendamentos encontrados.

**UC10: Gerenciar Especialidades Médicas**
- **Ator Principal:** Recepcionista
- **Objetivo:** Permitir que a recepcionista adicione, edite ou remova especialidades médicas no sistema.
- **Pré-condições:** A recepcionista deve estar autenticada.
- **Fluxo Principal:**
    1. A recepcionista seleciona a opção de gerenciar especialidades.
    2. O sistema exibe a lista de especialidades cadastradas.
    3. A recepcionista pode adicionar uma nova especialidade, editar uma existente ou remover uma especialidade.
    4. O sistema atualiza a lista de especialidades.
- **Pós-condições:** A lista de especialidades médicas é atualizada.

**UC11: Gerar Relatórios de Agendamento**
- **Ator Principal:** Recepcionista
- **Objetivo:** Permitir que a recepcionista gere relatórios sobre os agendamentos.
- **Pré-condições:** A recepcionista deve estar autenticada.
- **Fluxo Principal:**
    1. A recepcionista seleciona a opção de gerar relatórios.
    2. O sistema solicita os parâmetros do relatório (ex: período, médico, especialidade).
    3. A recepcionista informa os parâmetros.
    4. O sistema gera o relatório com base nos parâmetros e o exibe ou permite download.
- **Pós-condições:** Um relatório de agendamentos é gerado.

**UC12: Receber Notificações**
- **Ator Principal:** Paciente, Médico
- **Objetivo:** Permitir que pacientes e médicos recebam notificações sobre seus agendamentos.
- **Pré-condições:** O paciente/médico deve ter um agendamento ou uma alteração em um agendamento.
- **Fluxo Principal:**
    1. Uma ação no sistema (agendamento, cancelamento, edição) dispara uma notificação.
    2. O sistema envia a notificação (ex: e-mail, SMS) para o paciente e/ou médico.
    3. O paciente/médico recebe a notificação.
- **Pós-condições:** O paciente/médico é informado sobre a alteração no agendamento.

### 4.2. Diagrama de Classes

O Diagrama de Classes é uma representação estática da estrutura do sistema, mostrando as classes, seus atributos, métodos e os relacionamentos entre elas. Ele serve como um blueprint para a implementação do banco de dados e da lógica de negócios.

![Diagrama de Classes](https://private-us-east-1.manuscdn.com/sessionFile/pzZIAnZrjqX8BFcUID9SYs/sandbox/aqDI53yOy4zkekYVY5HdsS-images_1757424804526_na1fn_L2hvbWUvdWJ1bnR1L2NsYXNzX2RpYWdyYW0.png?Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9wcml2YXRlLXVzLWVhc3QtMS5tYW51c2Nkbi5jb20vc2Vzc2lvbkZpbGUvcHpaSUFuWnJqcVg4QkZjVUlEOVNZcy9zYW5kYm94L2FxREk1M3lPeTR6a2VrWVZZNUhkc1MtaW1hZ2VzXzE3NTc0MjQ4MDQ1MjZfbmExZm5fTDJodmJXVXZkV0oxYm5SMUwyTnNZWE56WDJScFlXZHlZVzAucG5nIiwiQ29uZGl0aW9uIjp7IkRhdGVMZXNzVGhhbiI6eyJBV1M6RXBvY2hUaW1lIjoxNzk4NzYxNjAwfX19XX0_&Key-Pair-Id=K2HSFNDJXOU9YS&Signature=ZSYwq0ORInHhppmpnOp~BQzAxBTQwGTGeQ0sJNs1N92OB1TtL4K8WVUiUmWitrXud8Wcaq1udaGtRPpJQOdpoeia4KVjAamuMV8UJ8IypMuz7fA1qyQKSQ1wNwKpQk7xCNkpTR7Av1HPgz1cAxXNUf3kVmzQw3gCNgChSZmnG6V4tJZVYHFEcwCFKFIyQCjOpLqAgg485QzAKz3E9oHERD58F5ApFACApwKSOn5cF8QPRtVcc9g2mPFwFQOEsMJp8NWDqb04mbOpcMmM1NMqdxj8nysqJGEfoZdo63j7YXdvsrEQSno-KuSYsaHi9M1rkX1h0E6e~EU~tGTyFUSiaw__)

### 4.3. Diagrama de Sequência

O Diagrama de Sequência ilustra a interação entre os objetos do sistema em uma ordem temporal, mostrando a sequência de mensagens trocadas para realizar uma funcionalidade específica. Abaixo, um exemplo para o caso de uso "Agendar Consulta".

![Diagrama de Sequência - Agendar Consulta](https://private-us-east-1.manuscdn.com/sessionFile/pzZIAnZrjqX8BFcUID9SYs/sandbox/aqDI53yOy4zkekYVY5HdsS-images_1757424804527_na1fn_L2hvbWUvdWJ1bnR1L3NlcXVlbmNlX2RpYWdyYW1fYWdlbmRhcl9jb25zdWx0YQ.png?Policy=eyJTdGF0ZW1lbnQiOlt7IlJlc291cmNlIjoiaHR0cHM6Ly9wcml2YXRlLXVzLWVhc3QtMS5tYW51c2Nkbi5jb20vc2Vzc2lvbkZpbGUvcHpaSUFuWnJqcVg4QkZjVUlEOVNZcy9zYW5kYm94L2FxREk1M3lPeTR6a2VrWVZZNUhkc1MtaW1hZ2VzXzE3NTc0MjQ4MDQ1MjdfbmExZm5fTDJodmJXVXZkV0oxYm5SMUwzTmxjWFZsYm1ObFgyUnBZV2R5WVcxZllXZGxibVJoY2w5amIyNXpkV3gwWVEucG5nIiwiQ29uZGl0aW9uIjp7IkRhdGVMZXNzVGhhbiI6eyJBV1M6RXBvY2hUaW1lIjoxNzk4NzYxNjAwfX19XX0_&Key-Pair-Id=K2HSFNDJXOU9YS&Signature=vz~UYDLM9Js~cdUup6LwJhaZPk-zxxbiK4IlLAa2sf7uZllq0BFOrxUQ15iln6PCNTJctWsW8jU9uxvCHWSLUxRqOS7-MdC2WW0n5fiqIajg5pRT77wiksY88mGRTNSq7gMKIt4B06KMXClbXrL3~Ox-kA~n4eUHktMQSaguIaNyeMqV8-nWVrpJBB00BriZN046N9BWkIQgjypaJS9noJ04SOuSvzwV-cks5KzQ02-RTXCp-DbSfIr8I0HaBQ-1DdtHHqHh~f7sJGLvFBeW-BhnB~6Gxlq132soJxApVigjjHUdmvncLz0gXqmE~QXKRrmaPzPIskKMG7aM~SPiyg__)



## 5. Conclusão

O processo de levantamento, análise e modelagem de requisitos é um pilar fundamental para o sucesso de qualquer projeto de desenvolvimento de software. Conforme demonstrado neste relatório, a dedicação a essas fases iniciais não apenas garante uma compreensão aprofundada das necessidades do negócio e dos usuários, mas também estabelece uma base sólida para a construção de um sistema robusto, eficiente e que realmente agregue valor.

A identificação clara dos requisitos funcionais e não funcionais, a priorização estratégica e a validação contínua com os stakeholders são essenciais para alinhar as expectativas e direcionar o desenvolvimento. A análise detalhada, que inclui a identificação e resolução de conflitos e a definição de critérios de aceitação precisos, minimiza ambiguidades e reduz significativamente o risco de retrabalho nas fases posteriores do projeto.

A modelagem do sistema, por meio de diagramas UML como Casos de Uso, Classes e Sequência, transforma conceitos abstratos em representações visuais e compreensíveis. Essa visualização facilita a comunicação entre a equipe de desenvolvimento e os usuários, permitindo que todos tenham uma visão compartilhada do sistema antes que uma única linha de código seja escrita. Além disso, a modelagem serve como um guia arquitetural, auxiliando na concepção de um design de software coeso e escalável.

Em suma, a aplicação rigorosa dessas práticas de engenharia de software nas etapas iniciais do projeto de agendamento de consultas médicas contribui diretamente para a qualidade final do sistema. Um sistema bem especificado e modelado é mais propenso a atender aos requisitos do usuário, ser entregue dentro do prazo e do orçamento, e ser mais fácil de manter e evoluir no futuro. Este relatório serve como um artefato crucial, documentando as decisões e o entendimento obtido, e pavimentando o caminho para uma implementação bem-sucedida.


