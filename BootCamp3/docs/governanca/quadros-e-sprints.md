# Quadros de acompanhamento e sprints

## Quadro Kanban

Use GitHub Projects (ou o quadro abaixo até sua configuração). Mover cartões somente quando a condição da coluna for satisfeita.

| Coluna | Regra de entrada/saída |
|---|---|
| **Backlog** | Issue descrita, mas ainda não priorizada. |
| **Pronta** | Prioridade, responsável e critérios de aceite definidos; dependências conhecidas. |
| **Em andamento** | Existe branch e responsável ativo; limite recomendado de 1–2 tarefas por pessoa. |
| **Em revisão** | PR aberta, checklist preenchido e testes executados. |
| **Bloqueada** | Impedimento descrito, com pessoa/ação necessária. |
| **Concluída** | PR integrada, CI verde, critérios verificados e Issue encerrada com evidência. |

## Papéis e responsabilidades

| Papel | Responsabilidade |
|---|---|
| Responsável pela Issue | Descrever o problema, critérios de aceite e confirmar resultado. |
| Autor da PR | Implementar, testar, documentar e responder à revisão. |
| Revisor | Verificar critérios, riscos, testes, privacidade e coerência documental. |
| Mantenedor | Configurar branches, permissões, merge e release. |
| Facilitador da sprint | Priorizar, acompanhar impedimentos e conduzir retrospectiva. |

Uma pessoa pode exercer mais de um papel ao longo do projeto, mas o autor não deve ser o único aprovador da própria PR.

## Modelo de sprint

Duração sugerida: 1 semana acadêmica ou o período acordado pelo grupo. Datas e participantes devem ser preenchidos antes do início; não inventar sprints retroativas.

### Planejamento
- Objetivo único e mensurável.
- Issues selecionadas e critérios de aceite revisados.
- Responsáveis, dependências e riscos.
- Capacidade real do grupo.

### Revisão de sprint
- Issues concluídas com links de PR e CI.
- Issues não concluídas e motivo, sem alterar retrospectivamente o status.
- Demonstração funcional ou evidência verificável.

### Retrospectiva
- O que funcionou?
- O que atrapalhou?
- Uma ou duas ações concretas para a próxima sprint, com responsável e prazo.

## Quadro de sprints — a preencher com dados reais

| Sprint | Período | Objetivo | Issues selecionadas | Resultado/evidências |
|---|---|---|---|---|
| S-01 | A definir | Implantar governança e privacidade | Candidatas GOV-01 a GOV-04 (criar no GitHub) | Não iniciada; sem evidência de execução |
| S-02 | A definir | Confirmar CI, proteção de branches e fluxo de PR | Candidatas GOV-05 a GOV-06 (criar no GitHub) | Não iniciada; sem evidência de execução |

**Definição de concluída:** aceite demonstrado; testes locais e CI relevantes aprovados; revisão independente concluída; documentação atualizada; PR integrada; Issue encerrada; evidências registradas.
