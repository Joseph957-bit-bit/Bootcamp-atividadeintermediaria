# Estratégia de branches e revisão

## Modelo recomendado

- `main`: versão estável/entregável; somente merge via PR aprovado.
- `develop`: integração da próxima entrega, se o grupo decidir mantê-la.
- `feature/<issue>-<slug>`: funcionalidade.
- `fix/<issue>-<slug>`: correção.
- `docs/<issue>-<slug>`: documentação.
- `test/<issue>-<slug>`: testes e infraestrutura de qualidade.
- `hotfix/<issue>-<slug>`: correção urgente originada de `main`.

Exemplos: `docs/12-governanca`, `feature/18-erro-estruturado`. Usar identificador real da Issue depois de ela existir; não usar números de exemplo como se fossem reais.

## Caminho de mudança

1. Criar Issue com problema, escopo, responsável e critérios de aceite.
2. Criar branch a partir da base acordada (`develop` para trabalho corrente, ou `main` se não houver `develop`).
3. Implementar em commits pequenos; atualizar especificação e changelog quando mudar contrato/regra.
4. Abrir PR, vincular Issue, preencher critérios e evidências.
5. Obter aprovação de outro integrante e CI verde.
6. Resolver comentários; se houver novos commits após aprovação, solicitar nova revisão.
7. Fazer merge pela estratégia definida pelo grupo e confirmar que a Issue foi encerrada automaticamente quando aplicável.
8. Excluir a branch de trabalho após merge, salvo necessidade documentada.

## Proteções recomendadas

Configurar no GitHub para `main` e, se existir, `develop`:
- exigir Pull Request;
- exigir pelo menos uma aprovação de pessoa diferente do autor;
- exigir conclusão bem-sucedida do workflow de testes;
- bloquear force-push e exclusão;
- exigir resolução de conversas;
- invalidar aprovações quando novos commits forem adicionados, se disponível;
- limitar quem pode fazer merge, conforme o tamanho do grupo.

O nome exato das opções pode variar no GitHub. Confirmar em Settings → Branches / Rulesets e registrar captura ou URL de configuração sem expor dados privados.

## Pronto para merge

- [ ] Critérios de aceite da Issue atendidos e demonstrados.
- [ ] Testes relevantes adicionados/atualizados e `python -m pytest` aprovado.
- [ ] CI verde no commit que será integrado.
- [ ] Pelo menos um revisor diferente do autor aprovou.
- [ ] Sem segredos, credenciais ou dados pessoais desnecessários no diff.
- [ ] Documentação, especificação e changelog atualizados quando aplicável.
- [ ] Riscos, migrações e limitações descritos.
