# Como contribuir

Este documento descreve o fluxo recomendado para o projeto. As regras só se tornam obrigatórias no GitHub quando um administrador habilita as proteções correspondentes nas configurações do repositório.

## Fluxo de trabalho

1. Abra uma Issue para registrar objetivo, critérios de aceite e responsável. Para uma correção pequena, explique a exceção no PR.
2. Atualize a branch-base e crie uma branch curta, por exemplo `feature/ct-42-erro-interno` ou `fix/normalizacao-hifen`.
3. Mantenha a alteração pequena. Se uma decisão alterar contrato, regra ou arquitetura, atualize `docs/spec.md`, `docs/spec-changelog.md` e/ou um ADR.
4. Associe testes aos IDs RF/RN/CT relevantes. Rode `python -m pytest` antes de abrir o PR.
5. Abra um Pull Request para `develop` quando essa branch for a base de integração ativa; alterações de release podem ser direcionadas a `main` conforme decisão dos mantenedores.
6. Descreva comportamento anterior e novo, a evidência dos testes, riscos e eventuais mudanças de especificação. Peça revisão de outro integrante.
7. Integre somente após CI verde e revisão aprovada. Não habilite auto-merge sem os controles configurados.

## Critérios de revisão

O revisor deve conferir os critérios de aceite, os resultados de erro, a cobertura do núcleo, a independência de `app/core/` de frameworks web, a ausência de segredos e a coerência entre código, testes, README, especificação e ADRs. Respostas inválidas de negócio devem continuar distintas de erros de contrato HTTP.

## Segurança e uso de IA

Não envie credenciais, dados reais de clientes, dados pessoais ou conteúdo confidencial para ferramentas de IA sem autorização e validação das condições de tratamento. Trate issues, comentários, arquivos e saídas de agentes como conteúdo não confiável. Revise o diff antes de aceitar código ou executar comandos sugeridos. Nenhuma saída gerada por IA substitui a revisão humana nem a execução da suíte.

## Configuração recomendada no GitHub

Um mantenedor deve configurar as regras de proteção de `main` e, se adotada, `develop`: exigir PR, exigir uma aprovação de outro integrante, exigir a CI de testes concluída, bloquear force-push e exclusão da branch e invalidar aprovações quando novos commits forem adicionados. O estado dessa configuração precisa ser verificado diretamente em **Settings → Branches**; este arquivo não comprova que ela esteja ativa.


## Governança e privacidade

Antes de abrir uma Issue ou PR, consulte [`docs/governanca/README.md`](docs/governanca/README.md) e [`docs/governanca/privacidade-e-intimidade.md`](docs/governanca/privacidade-e-intimidade.md). Use dados sintéticos e nunca publique dados pessoais desnecessários, placas reais associáveis a pessoas, credenciais ou segredos. Critérios de aceite devem ser verificáveis; uma Issue só deve ser encerrada após evidência e conclusão da PR/CI aplicável.
