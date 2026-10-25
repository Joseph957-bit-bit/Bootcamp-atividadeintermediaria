# Backlog inicial de governança — propostas de Issues

**Estado de todas as entradas:** candidatas para criação; não são Issues reais nem estão fechadas. Ao criar no GitHub, substituir os códigos locais por números reais e registrar links.

## GOV-01 — Configurar proteção de branches
**Prioridade:** alta | **Estimativa:** 2 pontos  
**Critérios de aceite**
- [ ] `main` exige PR para merge.
- [ ] Pelo menos uma aprovação independente é exigida.
- [ ] Workflow de testes é exigido e precisa estar verde.
- [ ] Force-push e exclusão da branch são bloqueados.
- [ ] Configuração verificada por mantenedor e evidência registrada.

## GOV-02 — Adotar política de privacidade e dados sintéticos
**Prioridade:** alta | **Estimativa:** 2 pontos  
**Critérios de aceite**
- [ ] Política revisada pelo grupo.
- [ ] README informa que a validação é sintática e não consulta proprietário/veículo.
- [ ] Testes e exemplos usam dados sintéticos.
- [ ] Checklist de privacidade incorporado ao template de PR.

## GOV-03 — Padronizar template de Issue
**Prioridade:** média | **Estimativa:** 1 ponto  
**Critérios de aceite**
- [ ] Template de bug pede passos de reprodução, resultado esperado/obtido e ambiente.
- [ ] Template de tarefa pede objetivo e critérios de aceite.
- [ ] Templates orientam a não incluir dados pessoais, credenciais ou segredos.

## GOV-04 — Implantar quadro de projeto e sprints
**Prioridade:** média | **Estimativa:** 2 pontos  
**Critérios de aceite**
- [ ] Quadro tem Backlog, Pronta, Em andamento, Em revisão, Bloqueada e Concluída.
- [ ] Cada item tem responsável e critérios de aceite.
- [ ] Sprint tem objetivo, período, Issues selecionadas e retrospectiva.
- [ ] Nenhum evento retroativo é declarado sem evidência.

## GOV-05 — Validar CI e cobertura no estado publicado
**Prioridade:** alta | **Estimativa:** 2 pontos  
**Critérios de aceite**
- [ ] Workflow roda em PR para a branch-base escolhida.
- [ ] Execução verde vinculada ao SHA da PR.
- [ ] `python -m pytest` passa.
- [ ] Limiar de cobertura configurado é respeitado.
- [ ] Falhas são corrigidas ou documentadas como bloqueio; não se registra sucesso sem execução.

## GOV-06 — Registrar primeira sprint com evidências
**Prioridade:** média | **Estimativa:** 3 pontos  
**Critérios de aceite**
- [ ] Datas e objetivo aprovados antes do início.
- [ ] Issues reais vinculadas à sprint.
- [ ] Revisão de sprint registra entregas e itens pendentes.
- [ ] Retrospectiva tem pelo menos uma ação com responsável e prazo.
- [ ] Links para PRs, Issues e CI foram verificados.

## Regra de encerramento de Issue

Encerrar somente quando os critérios de aceite forem verificados e a evidência for anexada ou vinculada. Se uma tarefa for cancelada, registrar motivo e decisão; não marcar como concluída apenas para limpar o quadro.
