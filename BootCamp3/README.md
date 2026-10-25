# Validador de Placas Brasileiras

API em Python para validar sintaticamente placas brasileiras nos padrões antigo (`ABC-1234`) e Mercosul (`ABC1D23`). A aplicação normaliza espaços externos e letras minúsculas, aceita hífen separador opcional e devolve um motivo estruturado quando a placa não corresponde às regras. A validação não consulta proprietário, RENAVAM, DETRAN nem confirma a existência ou regularidade do veículo.

O projeto é desenvolvido com *Spec-Driven Development* (SDD): requisitos, arquitetura, casos de teste e refinamentos estão registrados em [`docs/spec.md`](docs/spec.md), [`docs/components.md`](docs/components.md) e [`docs/spec-changelog.md`](docs/spec-changelog.md).

## Integrantes

- Adler Murga Ferreira — RA 22511624
- Alexandre Henrique Paiva Rocha — RA 22451424
- Arthur Gabriel da Silva Barbosa — RA 22500598
- Gabriel Francisco Pires de Assis — RA 22408417
- Jean de Almeida Brito — RA 22612228
- José Rafael de Lucena Martini — RA 22610479

## Arquitetura

O núcleo (`app/core/`) contém normalização, regras e resultado imutável e não depende de FastAPI ou Pydantic. `app/main.py` implementa a borda HTTP e `app/schemas.py` define os contratos de entrada e saída. A suíte `tests/` liga os casos parametrizados aos identificadores CT da especificação e testa também a API.

## API

| Método e rota | Resultado |
|---|---|
| `GET /` | Informações básicas do serviço. |
| `GET /health` | `200` com `{"status":"ok"}`. |
| `POST /validar` | `200` para placa válida ou inválida; uma placa inválida é resultado de negócio, não erro HTTP. |
| `GET /docs` | Documentação interativa OpenAPI do FastAPI. |
| `GET /openapi.json` | Esquema OpenAPI. |

Exemplo:

```bash
curl -X POST http://127.0.0.1:8000/validar \
  -H 'Content-Type: application/json' \
  -d '{"placa":"abc-1234"}'
```

Uma placa aceita retorna, por exemplo, `{"valida":true,"placa_normalizada":"ABC1234","padrao":"antigo","motivo":null,"mensagem":"Placa válida no padrão antigo."}`. Corpo ausente, JSON inválido ou campo `placa` de tipo incorreto retorna `422` com o objeto `erro` padronizado; método não permitido retorna `405`. Falhas internas são registradas como `500` sem expor detalhes da exceção na resposta.

## Executar localmente

Requisitos: Python 3.12 e Git. A versão de Docker necessária para os comandos da próxima seção é Docker Engine com `docker compose` v2.

```bash
git clone https://github.com/0GabrielF0/BootCamp3.git
cd BootCamp3
python -m venv .venv
```

Ative o ambiente virtual (`source .venv/bin/activate` no Linux/macOS ou `.venv\Scripts\Activate.ps1` no PowerShell) e instale dependências fixadas:

```bash
python -m pip install -r requirements.txt
python -m uvicorn app.main:app --reload
```

A API fica em `http://127.0.0.1:8000`; a interface OpenAPI fica em `/docs`. Encerre o servidor com `Ctrl+C`.

## Testes e cobertura

```bash
python -m pytest
```

O `pytest.ini` define a descoberta dos testes, relatório de cobertura do núcleo e falha automática se a cobertura ficar abaixo de 90%. Os casos CT-01 a CT-33 exercitam regras do núcleo; CT-34 a CT-42 cobrem contratos da API e a resposta segura a falha interna. A CI do GitHub Actions executa o mesmo comando em PRs direcionadas a `main` ou `develop`.

**Última execução local registrada nesta entrega (21/10/2026): 51 testes passaram e a cobertura observada em `app/core` foi 100%.** O ambiente em que essa execução ocorreu exibiu um aviso de depreciação do `TestClient` do Starlette em relação ao `httpx`; o aviso não falhou a suíte e deve ser acompanhado na próxima atualização de dependências. Este resultado é local, não é resultado de CI do GitHub.

## Docker Compose

Subir a API:

```bash
docker compose up --build
```

Executar o harness de testes em um container separado:

```bash
docker compose --profile test run --rm testes
```

O container da API publica a porta `8000`; o container de testes usa `Dockerfile.tests` e encerra com o código de saída do pytest. **A configuração foi adicionada, mas a execução do Docker Compose ainda precisa ser confirmada num host com Docker.**

## Git, contribuição e decisões

O fluxo proposto é `feature/*` → `develop` → `main`, com PR, CI verde e revisão por outro integrante antes do merge. Consulte [`CONTRIBUTING.md`](CONTRIBUTING.md) para o processo e [`docs/adr/`](docs/adr/) para as decisões de arquitetura. As instruções documentam o processo desejado; a exigência de aprovação e as regras de proteção precisam estar habilitadas nas configurações do repositório GitHub para serem obrigatórias.

## Entrega 2

O relatório técnico-ético e a comparação documental das ferramentas de IA estão em [`docs/relatorio-entrega-2.md`](docs/relatorio-entrega-2.md). A situação de integração e as pendências que dependem de acesso ao GitHub/Docker estão em [`docs/evidencias-entrega-2.md`](docs/evidencias-entrega-2.md).


## Governança, privacidade e acompanhamento

O pacote de governança proposto está em [`docs/governanca/README.md`](docs/governanca/README.md). Ele define fluxo de branches e PRs, critérios de aceite, templates de Issues, proteção de privacidade/intimidade, quadro Kanban e modelo de sprints. As Issues e sprints listadas são propostas, não eventos históricos comprovados. Consulte [`docs/governanca/registro-evidencias.md`](docs/governanca/registro-evidencias.md) para distinguir evidências documentadas de pendências de publicação.
