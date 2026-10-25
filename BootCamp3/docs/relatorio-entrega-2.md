# Entrega 2 — Relatório técnico-ético

**Projeto:** Validador de Placas Brasileiras | **Data:** 21/10/2026 | **Situação:** minuta técnica preparada com assistência de IA para revisão e autoria final do grupo.

## Refinamento técnico e decisões

O escopo permaneceu como validação sintática: receber texto, normalizar casos definidos, aplicar as máscaras antigas e Mercosul e retornar resultado estruturado. A solução não consulta cadastros nem afirma que a placa existe. Isso mantém o sistema pequeno, determinístico e sem integração externa.

A separação entre núcleo e API permite testar as regras sem subir o servidor. O núcleo não depende de FastAPI ou Pydantic; a camada HTTP traduz JSON para o resultado de domínio. Essa divisão é protegida por um teste de arquitetura. A decisão evita que um framework se torne parte do contrato das regras, embora exija uma conversão explícita dos enums e modelos para JSON.

A resposta `200` para placa inválida foi mantida porque a requisição pode ter sido processada corretamente e ainda assim não satisfazer uma regra de domínio. O cliente deve avaliar `valida`. Já corpo JSON inválido, campo ausente ou tipo incompatível retorna `422`; método incorreto retorna `405`; uma falha interna responde `500` sem expor a exceção. Os testes cobrem essas fronteiras.

A normalização é deliberadamente restrita: remove espaços das extremidades, converte para maiúsculas e retira um único hífen separador na posição definida. Não apaga espaços internos, acentos ou pontuação. A ordem de rejeição torna `motivo` previsível. Alterações futuras nesses comportamentos devem ser precedidas por refinamento da especificação e novos casos de teste.

## Testes e resultado observado

Na execução local de 21/10/2026, em Python 3.12.3, pytest 9.1.1 e pytest-cov 7.1.0, foram aprovados **51 testes**, com **100% de cobertura observada em `app/core/`**. O limite automatizado ficou em 90%. A suíte identifica os casos CT-01 a CT-41 e acrescenta CT-42 para assegurar que uma exceção interna não seja devolvida ao cliente.

Essa evidência não substitui a CI do GitHub. A execução mostrou um aviso de depreciação na integração entre `TestClient` do Starlette e `httpx`; não houve falha. O ambiente de trabalho não tinha Docker disponível, por isso a nova configuração Compose e o harness em container não foram executados. Os resultados precisam ser confirmados num host com Docker.

## Comparação documental de ferramentas de programação com IA

A matriz compara capacidades e controles declarados nas documentações oficiais consultadas em 21/10/2026. É uma comparação documental, não um benchmark do validador nem evidência de que o grupo tenha usado todas essas ferramentas. Controles, retenção e disponibilidade variam conforme produto, plano, configuração e conta.

| Ferramenta | Fluxo de trabalho e utilidade potencial neste projeto | Controles e dados a considerar |
|---|---|---|
| **Claude Code** | Agente para terminal/IDE que pode ler o repositório, editar arquivos e executar comandos; encaixa em correções que precisam rodar testes locais. | A documentação descreve arquitetura baseada em permissões e sandbox, mas comandos aprovados podem ter alcance maior que a fronteira de arquivos. Políticas de treinamento e retenção diferem entre contas de consumo e comerciais; há ainda cache local de sessões. Conferir permissões e configurações antes de usar em código sensível. [1] [2] |
| **OpenAI Codex CLI** | Agente de terminal adequado a tarefas de manutenção e execução controlada de comandos em workspace. | A OpenAI descreve sandbox como limite técnico para escrita/rede e aprovações como controle para ações fora do limite. O artigo consultado também descreve controles gerenciados de rede e auditoria organizacional; não se deve supor que a configuração corporativa seja o padrão de toda conta individual. [3] |
| **Cursor** | Ambiente IDE com assistência de código e agentes, útil quando o grupo prefere revisar alterações no editor e trabalhar por diffs. | A página do fornecedor afirma que Privacy Mode impede uso para treinamento e descreve acordos ZDR para provedores, mas a solicitação ainda passa pelo backend do Cursor e pode haver processamento/cache temporário. Com o modo desativado, código, prompts e ações podem ser armazenados ou usados para melhoria conforme a política. Confirmar modo e provedor escolhido. [4] |
| **Google Antigravity** | Superfícies desktop, CLI, extensões de IDE e SDK; documenta fluxos de agentes síncronos e tarefas em segundo plano, inclusive coordenação de subagentes. | A documentação descreve permissões granulares com listas `Deny`, `Ask` e `Allow` para ações sensíveis. Mais autonomia amplia a importância de escopo de projeto, revisão de diff, atenção a comandos e configuração explícita das permissões. [5] [6] |

Não há ferramenta vencedora universal para este projeto. Para tarefas curtas e determinísticas, qualquer opção só agrega valor se produzir alterações pequenas, explicáveis e reproduzíveis, sem quebrar a especificação. Para contexto confidencial, a decisão depende da política da organização e do tratamento de dados configurado; nenhuma descrição comercial substitui leitura dos termos aplicáveis à conta.

## Avaliação ética, limites e segurança

**Código inseguro ou incorreto.** Um modelo pode propor regex permissiva, tratar mal caracteres Unicode, confundir placa sintaticamente válida com veículo existente ou criar um tratamento de erro que exponha detalhes. Mitigação: critérios da especificação, revisão linha a linha, casos negativos, CI, verificação de dependências e teste de que `app/core/` segue independente. O guia OWASP recomenda avaliar saída do agente, tratar conteúdo do repositório como não confiável e aplicar verificações de segurança específicas para sistemas de codificação com IA. [7]

**Vazamento de dados e confidencialidade.** O código e os prompts podem incluir informações que não deveriam sair do ambiente. O princípio da necessidade da LGPD limita dados pessoais ao mínimo adequado à finalidade; segurança e prevenção também exigem medidas técnicas e administrativas. Uma placa isolada não é automaticamente tratada aqui como identificador de proprietário, mas, quando vinculada ou associável a uma pessoa natural, o contexto pode envolver dado pessoal. O validador não precisa de dados reais de veículos para testar. Use exemplos sintéticos e nunca envie credenciais, `.env`, tokens, informações identificáveis ou código confidencial a um serviço sem autorização e avaliação dos termos. [8]

**Propriedade intelectual e licenças.** A origem de trechos gerados pode ser opaca, e regras variam por ferramenta e contrato. A equipe deve revisar dependências e código copiado, manter licenças e atribuições exigidas e evitar aceitar blocos cuja origem ou compatibilidade com a licença do repositório não possa ser avaliada. Esta análise é um controle de processo, não uma opinião jurídica.

**Injeção de prompt e conteúdo não confiável.** Issues, README, comentários de código, saídas de teste e páginas externas podem conter instruções maliciosas. Um agente não deve interpretá-las como autorização. Restringir diretórios e permissões, não fornecer segredos, pedir confirmação para efeitos externos e inspecionar alterações antes de executar são controles práticos. O guia OWASP chama atenção para prompt injection, alterações inesperadas e caracteres invisíveis em conteúdo processado por agentes. [7]

**Responsabilidade humana e auditabilidade.** A decisão de aceitar, revisar e integrar código continua com os integrantes. Guardar o diff, commits, PR, resultado dos testes e justificativas cria trilha de auditoria. A IA não deve ser apresentada como autora da decisão de negócio nem como garantia de segurança.

## Relato de experiência e defesa técnica

Nesta preparação, a IA foi usada como apoio para inspecionar o repositório, mapear lacunas entre a especificação e os testes, propor alterações de rastreabilidade, executar a suíte no ambiente disponível e preparar documentação. O grupo ainda precisa revisar todo o diff, validar as decisões, atribuir a autoria acadêmica final e executar os comandos em Docker. Não há evidência nos arquivos consultados de que a equipe tenha testado Claude Code, Codex CLI, Cursor e Antigravity; portanto, a comparação acima não é apresentada como experiência prática com esses quatro produtos.

A experiência mais relevante para a defesa é que regras claras viram testes rastreáveis. A cobertura de 100% no núcleo demonstra que as linhas de código foram exercitadas por essa suíte, mas não prova ausência de defeitos nem valida a integração Docker ou a publicação. Essa distinção evita tratar uma métrica como garantia total de qualidade.

### Slide-síntese para apresentar

**Título:** Do requisito à evidência — Validador de Placas Brasileiras

- **Problema:** validação inconsistente entre placa antiga e Mercosul.
- **Decisão:** núcleo puro separado da API FastAPI; rejeições com motivo estável; erros de contrato separados dos erros de negócio.
- **Evidência local:** 51 testes aprovados; 100% de cobertura no núcleo; casos CT rastreados à especificação.
- **Limite atual:** Docker e CI remota ainda precisam de execução/validação; integração depende da revisão e publicação da branch.
- **Uso responsável de IA:** exemplos sintéticos, sem segredos, diff revisado por pessoas e testes antes de integrar.

**Fala sugerida:** “Partimos de regras explícitas para dois formatos de placa e separamos a validação de domínio da API. A suíte liga os casos CT aos requisitos e, nesta execução local, todos os 51 testes passaram, com 100% de cobertura do núcleo. Isso não substitui revisão nem prova que o container ou a CI remota já funcionem: esses pontos ainda precisam ser confirmados pelo grupo. A IA ajudou a preparar análise e alterações, mas a decisão e a integração precisam de revisão humana.”

## Referências

[1]: https://code.claude.com/docs/en/security "Security - Claude Code Docs"
[2]: https://code.claude.com/docs/en/data-usage "Data usage - Claude Code Docs"
[3]: https://openai.com/index/running-codex-safely/ "Running Codex safely at OpenAI"
[4]: https://cursor.com/data-use "Cursor Data Use & Privacy Overview"
[5]: https://antigravity.google/docs/overview/ "Choose your Antigravity"
[6]: https://antigravity.google/docs/permissions/ "Permissions - Google Antigravity Docs"
[7]: https://cheatsheetseries.owasp.org/cheatsheets/Secure_Coding_with_AI_Cheat_Sheet.html "Secure Coding with AI - OWASP Cheat Sheet Series"
[8]: https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm "Lei Geral de Proteção de Dados Pessoais Lei nº 13.709 de 14 de agosto de 2018"
