# Evidências e pendências — Entrega 2

**Data da verificação:** 21/10/2026

**Repositório:** [0GabrielF0/BootCamp3](https://github.com/0GabrielF0/BootCamp3)

## Evidências locais desta preparação

- Implementação existente na branch remota `feature/validador-placas`; a branch remota `main` não contém ainda a implementação observada.
- Alterações desta etapa preparadas na branch local `feature/entrega-2`, baseada na branch de implementação.
- `python -m pytest`: **51 testes aprovados**, sem falhas.
- Cobertura observada em `app/core/`: **100%** (limiar automático configurado em 90%).
- Os testes agora exibem IDs CT-01 a CT-41 e verificam o caso adicional CT-42 de falha interna sem vazamento do detalhe da exceção.
- Foram incluídos comandos de execução, dependências com versões fixas, perfil de testes no Compose, workflow de CI, template de PR, guia de contribuição, ADRs e relatório técnico-ético.

O relatório da execução local exibiu um aviso de depreciação do `TestClient` do Starlette em relação ao `httpx`. Não causou falha. A compatibilidade deve ser reavaliada ao atualizar as dependências.

## Governança remota observada

Na consulta pública ao GitHub, a PR [#9 — implementação do validador e testes](https://github.com/0GabrielF0/BootCamp3/pull/9) estava aberta com destino a `main` e origem `feature/validador-placas`. Isso mostra que a funcionalidade ainda aguardava integração na data da consulta. As PRs #7 e #8 estavam encerradas.

O clone deste trabalho não tinha sessão autenticada da GitHub CLI. Por isso, as alterações da branch local não foram enviadas, uma nova PR não foi aberta e não foram alteradas configurações remotas de proteção, revisores, Issues ou Projects. O `CONTRIBUTING.md` e o template de PR são propostas versionadas, não evidências de que as regras já estão impostas no GitHub.

## Pendências antes da entrega publicada

1. Um mantenedor autentica no GitHub e publica `feature/entrega-2`.
2. O grupo decide se essa branch deve seguir como atualização da PR #9 ou como PR separada; avaliar se a base será `main` ou `develop` conforme o fluxo adotado.
3. Revisar e aprovar a PR por outro integrante, conferir a CI verde e integrar a implementação e os documentos.
4. Configurar e testar proteção de branch, revisão obrigatória e exigência da CI. Registrar Issue/Project para as tarefas se a disciplina exigir essa evidência.
5. Em máquina com Docker, executar `docker compose up --build` e `docker compose --profile test run --rm testes`; registrar os resultados reais.
6. Confirmar no GitHub que a API/documentação e os arquivos finais estão publicados e que o status do workflow está verde.

**Conclusão:** o material de código e documentação foi preparado e verificado localmente, mas a publicação/integração remota, a configuração de governança do repositório e a execução em Docker permanecem pendentes de ação de um mantenedor e de um host com Docker.
