# Changelog da Especificação — Validador de Placas Brasileiras

Registro de refinamentos da especificação técnica ([`spec.md`](./spec.md) e
[`components.md`](./components.md)) feitos a partir de feedback do grupo, revisão de PR ou
resultado de testes. Atende ao item **"Refinamento por Feedback"** da Entrega 1.

## Como registrar uma alteração

1. Toda mudança na spec entra por PR, junto com a alteração no documento.
2. Adicione uma nova seção no **topo** da lista de versões (ordem cronológica inversa).
3. Use versionamento semântico do documento:
   - **MAIOR** (`2.0`): mudança que quebra contrato já implementado (rota, formato de
     resposta, semântica de regra existente).
   - **MENOR** (`1.1`): novo RF/RNF/RN ou novo caso de teste, sem quebrar o que existe.
   - **CORREÇÃO** (`1.0.1`): correção de texto, exemplo ou erro de digitação.
4. Nunca reutilize um ID (RF/RNF/RN/CT) aposentado. Marque-o como `OBSOLETO` e crie um novo.
5. Sempre preencha o **motivo** e o **impacto nos testes**.

### Modelo de entrada

```markdown
## vX.Y — AAAA-MM-DD

**Origem:** (revisão de PR #N | falha no teste CT-NN | decisão em reunião | professor)
**Autor:** Nome

**O que mudou**
- ...

**Motivo**
- ...

**Impacto**
- IDs afetados: ...
- Testes a criar/ajustar: ...
- Código a ajustar: ...
```

---

## v1.1 — 2026-10-21

**Origem:** refinamento da suíte e do harness para a Entrega 2.
**Autor:** Manus AI (minuta preparada para revisão e aceite do grupo).

**O que mudou**

- Inclusão do CT-42 para verificar que falha interna simulada retorna `500` com `ERRO_INTERNO`, sem mensagem da exceção ou stack trace.
- Rastreabilidade explícita CT-01 a CT-41 nos testes parametrizados da suíte; revisão da decomposição para refletir os caminhos reais `app/schemas.py` e `app/main.py`.
- Harness de cobertura com limiar de 90%, versões diretas fixadas, perfil opcional de teste no Docker Compose, e CI executando pytest.
- README, instruções de contribuição, template de PR, ADRs e relatório técnico-ético preparados para revisão.

**Motivo**

- Fechar a evidência para tratamento seguro de falhas internas e aproximar a documentação da implementação observada.
- Permitir que testes e cobertura sejam executados por um comando comum, localmente, na CI ou no perfil Docker.

**Impacto**

- IDs afetados: CT-42; RF-08, RNF-01, RNF-05 e RNF-09 como critérios de rastreabilidade e segurança.
- Testes a criar/ajustar: `tests/test_api.py::test_erro_interno_nao_expoe_detalhes_CT42`; associar os testes existentes aos IDs CT-01 a CT-41.
- Código a ajustar: sem alteração nas regras de domínio; atualizar configuração de CI, ambiente de teste e documentação. A validação no Docker e a publicação remota continuam pendentes.

---

## v1.0 — 2026-09-12

**Origem:** especificação inicial da Entrega 1 (Spec-Driven Development).
**Autor:** Adler Murga Ferreira (RA 22511624)

**O que mudou**

- Criação de `docs/spec.md`: descrição do problema, escopo e não-objetivos, 10 requisitos
  funcionais (RF-01 a RF-10), 10 requisitos não-funcionais (RNF-01 a RNF-10), 12 regras de
  negócio (RN-01 a RN-12), contratos da função núcleo e da API (`POST /validar`,
  `GET /health`) e 41 casos de teste (CT-01 a CT-41).
- Criação de `docs/components.md`: decomposição em seis unidades (C1 normalizador,
  C2 validador núcleo, C3 modelo de resultado, C4 schemas Pydantic, C5 camada API,
  C6 tratador de erros), interfaces entre elas e diagramas Mermaid.
- Criação deste changelog.

**Decisões registradas**

- Placa inválida responde `200` com `valida: false`; `422` fica reservado a erro de
  contrato HTTP. Motivo: separar "requisição malformada" de "resposta de negócio negativa".
- O núcleo de validação não importa FastAPI nem Pydantic (RNF-01), com teste de arquitetura
  como guarda. Motivo: permitir testar e reutilizar as regras sem subir servidor.
- O motivo da rejeição é um código fechado (`Motivo`), não texto livre. Motivo: permitir que
  os testes referenciem a regra violada de forma estável.
- Validação é apenas sintática; consulta a bases oficiais fica fora do escopo. Motivo:
  manter a Entrega 1 sem dependência externa e com testes determinísticos.

**Impacto**

- IDs afetados: todos (versão inicial).
- Testes a criar: `tests/test_normalizador.py`, `tests/test_validador.py`,
  `tests/test_api.py`, `tests/test_arquitetura.py`.
- Código a criar: `app/core/` (C1–C3) e `app/api/` (C4–C6).

---

## Pendências conhecidas (candidatas a v1.2)

| Item | Descrição | Disparador |
|---|---|---|
| P-01 | Endpoint de validação em lote (`POST /validar-lote`). | Se surgir requisito de importação de planilha. |
| P-02 | Regra para placas de motocicleta / formatos especiais. | Feedback do professor ou do grupo. |
| P-03 | Aceitar separador diferente de hífen (espaço, ponto). | Se os testes apontarem entrada real nesse formato. |
| P-04 | Internacionalização das mensagens. | Fora do escopo enquanto RNF-07 valer. |
