# Pacote de Governança — Validador de Placas

**Versão:** 1.0 | **Preparado em:** 23/10/2026  
**Estado:** proposta pronta para revisão do grupo; ainda não aplicada ao GitHub.

Este pacote acrescenta processos, modelos e quadros para branches, Issues, Pull Requests (PRs), sprints, segurança e privacidade. Ele **não altera nem inventa o histórico remoto**. O ZIP recebido não contém a pasta `.git`; portanto, não permite comprovar commits, autores, datas de merge, sprints executadas ou Issues fechadas. Os itens de planejamento estão identificados como propostas até que sejam criados e atualizados no repositório remoto.

## Índice

- [`fluxo-branches.md`](fluxo-branches.md): estratégia de branches e controles de merge.
- [`privacidade-e-intimidade.md`](privacidade-e-intimidade.md): tratamento de dados, direitos e resposta a incidentes.
- [`quadros-e-sprints.md`](quadros-e-sprints.md): quadros Kanban, papéis, sprints e critérios de conclusão.
- [`registro-evidencias.md`](registro-evidencias.md): separação entre fatos verificados, histórico informado no documento-base e pendências de prova.
- [`backlog-inicial.md`](backlog-inicial.md): Issues candidatas com critérios de aceite; não afirmar como fechadas antes de evidência real.
- `../../.github/ISSUE_TEMPLATE/`: modelos de Issue.
- `../../.github/PULL_REQUEST_TEMPLATE.md`: modelo de PR com critérios de aceite e privacidade.

## Adoção

1. O grupo revisa e aprova os documentos.
2. Um mantenedor cria as Issues reais e atribui responsáveis e milestones/sprints.
3. O grupo configura proteção de branches e regras de aprovação em Settings do GitHub.
4. PRs reais vinculam Issues (`Closes #N`) e registram testes, revisão e evidência de CI.
5. Após cada sprint, atualiza-se o quadro e registra-se retrospectiva com data e participantes.
6. O relatório de evidências é atualizado com URLs/IDs reais e resultados observados.

**Importante:** documentação versionada é uma proposta de processo; por si só, não prova que uma configuração remota esteja ativa.
