# Registros de Decisões Arquiteturais (ADRs)

Os registros abaixo documentam decisões refletidas na implementação. Devem ser discutidos e aceitos pelo grupo antes do merge final. O status “Aceita tecnicamente” descreve a decisão no projeto; não representa aprovação de um Pull Request.

## ADR-001 — Núcleo de domínio independente da API

**Status:** Aceita tecnicamente

**Contexto:** A regra de validação deve ser testável sem servidor HTTP e reutilizável por outros adaptadores.

**Decisão:** Manter normalização, modelos de resultado e validação em `app/core/`, sem importar FastAPI, Pydantic ou Starlette.

**Alternativas consideradas:** Colocar regra e serialização em uma rota FastAPI; dividir o validador em classes com dependências web.

**Justificativa:** A função pura reduz acoplamento, simplifica testes de unidade e permite que a camada HTTP seja substituída sem reescrever as regras. Um teste de arquitetura protege essa fronteira.

**Consequências:** A API precisa mapear os enums e dataclass para JSON; regras não devem ser duplicadas nos schemas ou endpoints.

**Evidência:** `app/core/`, `tests/test_validator.py` e RNF-01 em `docs/spec.md`.

## ADR-002 — Resultado de negócio inválido é diferente de erro HTTP

**Status:** Aceita tecnicamente

**Contexto:** Uma requisição pode estar bem formada e ainda conter uma placa incompatível com os formatos.

**Decisão:** `POST /validar` responde `200` com `valida: false` e código `motivo` para resultado de negócio inválido. Falha do contrato JSON usa `422`; método não permitido usa `405`; falha interna usa `500` com corpo genérico.

**Alternativas consideradas:** Responder `4xx` para toda placa inválida; lançar exceção de validação do framework no núcleo.

**Justificativa:** O status HTTP descreve o processamento da requisição, enquanto `valida` descreve a conclusão da regra de domínio. Isso preserva um resultado uniforme para consumidores da API.

**Consequências:** Clientes precisam verificar `valida`, não apenas o status `200`. Testes cobrem ambas as categorias e confirmam que erro interno não expõe a exceção.

## ADR-003 — Normalização explícita, seguida de validação estrita

**Status:** Aceita tecnicamente

**Contexto:** Espaços externos e letras minúsculas são erros de apresentação recuperáveis, mas espaços internos, acentos e pontuação podem mascarar entradas incorretas.

**Decisão:** Aplicar `strip`, converter para maiúsculas e remover somente um hífen na quarta posição quando a entrada tem oito caracteres. Não transliterar acentos nem apagar outros caracteres. Em seguida, conferir tamanho, conjunto permitido e máscaras exatas em ordem determinística.

**Alternativas consideradas:** Remover toda pontuação; retirar acentos; aceitar espaços internos; usar uma única regex com erro genérico.

**Justificativa:** A normalização documentada mantém o resultado canônico e evita transformar entradas ambíguas em placas aparentemente válidas. A ordem de rejeição produz motivos reproduzíveis.

**Consequências:** Novas variantes de entrada exigem alteração explícita da especificação e dos casos de teste.

## ADR-004 — Testes automatizados como critério de integração

**Status:** Aceita tecnicamente

**Contexto:** As regras e os contratos precisam continuar cobertos durante mudanças colaborativas.

**Decisão:** Usar pytest, rastreabilidade dos cenários CT e um limiar de cobertura de 90% para `app/core/`; a CI executa a suíte em PRs para `main` e `develop`. Um perfil de teste no Compose oferece a mesma suíte em container.

**Alternativas consideradas:** Teste manual sem evidência; cobertura sem bloqueio; executar API e teste em uma mesma imagem.

**Justificativa:** A CI fornece uma verificação repetível, e o serviço de testes fica separado do contêiner de runtime.

**Consequências:** O grupo ainda precisa verificar a execução real no Docker e configurar regras de branch que tornem a aprovação da CI obrigatória.
