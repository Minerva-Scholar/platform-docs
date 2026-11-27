# Minerva — Documentação da Plataforma (`platform-docs`)

Repositório da documentação técnica do sistema **Minerva**, publicada como site estático com [Zensical](https://zensical.org).

- **Site:** `https://minerva-scholar.github.io/platform-docs/`
- **Repositório:** `https://github.com/Minerva-Scholar/platform-docs`

---

## Como executar localmente

**Pré-requisitos:** Python `>= 3.12` com `zensical==0.1.3` instalado (ou [`uv`](https://docs.astral.sh/uv/)).

A partir da raiz de `platform-docs/`:

```bash
# Servidor local com recarregamento automático
python -m zensical serve

# Build estático limpo (validação obrigatória antes de commits)
python -m zensical build --clean
```

Com `uv`, substitua `python -m` por `uv run`:

```bash
uv run zensical serve
uv run zensical build --clean
```

> **Estado atual (mutável):** o ambiente local utiliza `python -m zensical` diretamente; `pyproject.toml` já está preparado para `uv` (`package = false`).

---

## Onde fica cada coisa

- `docs/` — conteúdo publicado pelo Zensical.
- `zensical.toml` — configuração do site, tema, extensões e navegação.
- `pyproject.toml`, `uv.lock` e `.python-version` — dependências e versão do Python (`uv`).
- `.github/workflows/` — build e publicação automática no GitHub Pages.

---

## Como contribuir

Leia o guia completo em [docs/contributing/documentation.md](docs/contributing/documentation.md). Em resumo:

- **Decisão:** documentação sempre em português do Brasil (`pt-BR`, com acentos); código e nomes de arquivos/caminhos em inglês.
- **Decisão:** texto direto, conciso, orientado a fatos e com marcação explícita do que é **Decisão** e do que é **Estado atual (mutável)**.
- **Decisão:** commits atômicos e compiláveis (`python -m zensical build --clean` sem erros) em Conventional Commits.
