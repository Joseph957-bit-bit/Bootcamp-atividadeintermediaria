# Registro de evidências e trilha de auditoria

**Preparado em:** 23/10/2026. Este registro separa observações do pacote recebido de eventos que ainda precisam ser comprovados no GitHub.

## Evidências que constam no documento-base

O arquivo `docs/evidencias-entrega-2.md`, datado de 21/10/2026, informa que:
- uma execução local registrou 51 testes aprovados e 100% de cobertura observada em `app/core/`;
- a PR #9 de implementação foi observada aberta, e as PRs #7 e #8 encerradas;
- as alterações da Entrega 2 não foram enviadas ao remoto naquele momento;
- a configuração remota de proteção de branches, Issues/Projects e a execução Docker permaneciam pendentes.

Esses itens são **declarações documentadas no arquivo-base**, não uma nova verificação independente feita durante a criação deste pacote. Consulte o documento-base e confirme o estado atual no repositório antes de usar como status atual.

## O que não pode ser declarado como comprovado neste pacote

- que uma branch foi criada ou protegida remotamente nesta atualização;
- que novas PRs foram abertas, aprovadas ou mergeadas;
- que Issues candidatas foram criadas ou fechadas;
- que sprints ocorreram, com datas, participantes e resultados;
- que a CI ou Docker executaram com sucesso nesta atualização.

O ZIP não inclui `.git`, logs de eventos nem exportação do GitHub. Portanto, não é possível reconstruir um histórico Git autêntico somente a partir dele.

## Modelo de evento auditável

| Data/hora (UTC) | Tipo | ID/URL real | Autor/responsável | Estado | Evidência | Observação |
|---|---|---|---|---|---|---|
| A preencher | PR / Issue / sprint / CI / branch | Link real | Nome/usuário autorizado | Estado real | URL de execução, commit ou registro | Sem dados pessoais desnecessários |

## Como produzir histórico comprovável

1. Publique os arquivos em uma branch real, sem substituir o histórico existente.
2. Abra PR para a base acordada; a PR fornece commits, autorias, revisões, status de CI e data de merge.
3. Crie Issues no GitHub com critérios de aceite e vincule-as às PRs por `Closes #N`.
4. Use milestones ou GitHub Projects para sprints; registre datas, objetivo, itens selecionados e retrospectiva.
5. Registre o link de cada workflow e o SHA do commit testado.
6. Exporte ou capture a configuração de proteção de branches, ocultando dados privados.
7. Atualize este registro somente após observar as evidências. Não retroagir datas nem marcar trabalho proposto como concluído.

## Critério de integridade

Um histórico é comprovado quando cada afirmação de status tem um identificador verificável (commit, PR, Issue, execução de CI ou registro de sprint) e a evidência sustenta exatamente o que se afirma. Uma tabela preenchida manualmente sem links não substitui a trilha remota.
