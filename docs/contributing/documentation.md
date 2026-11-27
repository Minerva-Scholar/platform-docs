# Como Contribuir para a Documentação

Este guia define as regras, convenções e o fluxo de trabalho para escrever e manter a documentação do projeto **Minerva**.

---

## 1. Princípios de Escrita

!!! info "Decisão"
    Toda página da documentação segue quatro regras permanentes:

    1. **Simples, direta e concisa, mas completa:** vá direto ao ponto sem omitir pré-requisitos, comandos ou restrições importantes. Evite adjetivos vagos e texto de preenchimento.
    2. **Orientada a fatos:** documente o que existe, o que foi medido e o que foi decidido. Nunca invente métricas, benchmarks ou resultados — toda medição precisa ser reprodutível.
    3. **Status explicitamente declarado:** deixe claro o que é **Decisão** (estável), o que é **Estado atual (mutável)** (sujeito a mudança) e o que está **Em aberto** (aguardando definição).
    4. **Idioma:** texto em **português do Brasil (`pt-BR`, com acentuação correta)**; nomes de arquivos, diretórios, identificadores, comandos e trechos de código sempre em **inglês**.

---

## 2. Como Declarar Decisões e Estado Mutável

Use rótulos explícitos (via *admonitions* do Zensical ou marcação em negrito) para separar fatos estáveis de condições temporárias:

| Classificação | Quando usar | Bloco sugerido |
| --- | --- | --- |
| **Decisão** | Regra acordada, padrão técnico ou escolha arquitetural vigente. | `!!! info "Decisão"` |
| **Estado atual (mutável)** | Configuração temporária, limitação do momento ou estrutura ainda em evolução. | `!!! warning "Estado atual (mutável)"` |
| **Em aberto** | Ponto conhecido que ainda aguarda escolha ou validação. | `!!! question "Em aberto"` |

Exemplo de uso em Markdown:

```markdown
!!! info "Decisão"
    O gerador de documentação oficial do projeto é o Zensical.

!!! warning "Estado atual (mutável)"
    O build é executado localmente com `python -m zensical build --clean`. A pipeline de CI para publicação automática ainda será configurada.
```

---

## 3. Estrutura e Organização

!!! info "Decisão"
    Todo conteúdo publicado reside em `docs/` e é exposto na navegação via `zensical.toml`.

- **Caminhos e arquivos:** use inglês em `kebab-case` (ex.: `docs/contributing/documentation.md`, `docs/architecture/data-model.md`).
- **Títulos e navegação:** use `pt-BR` nos cabeçalhos (`# ...`) e nos rótulos de `nav` em `zensical.toml`.
- **Inclusão na navegação:** ao criar uma página nova, registre-a no bloco `nav` de `zensical.toml` para que apareça no menu lateral.
- **Diretórios gerados:** nunca versione `site/` nem `.cache/` (ambos já constam no `.gitignore`).

!!! warning "Estado atual (mutável)"
    O site está em fase inicial de estruturação, com apenas `index.md` e `contributing/documentation.md` publicados. Novos domínios (arquitetura, serviços, operação, ADRs) serão adicionados conforme decididos.

---

## 4. Recursos de Markdown Disponíveis

As extensões abaixo estão habilitadas em `zensical.toml` e podem ser usadas diretamente:

- **Admonitions e blocos expansíveis:** `!!! tipo "Título"` e `??? tipo "Título"` (`admonition`, `pymdownx.details`).
- **Diagramas Mermaid:** blocos cercados com ```` ```mermaid ```` (`pymdownx.superfences`).
- **Abas de conteúdo:** `=== "Aba 1"` (`pymdownx.tabbed`).
- **Código com destaque e cópia:** blocos com linguagem declarada, numeração de linhas e botão de cópia (`pymdownx.highlight`).
- **Tabelas, listas de tarefas e notas de rodapé:** `tables`, `pymdownx.tasklist`, `footnotes`.
- **Fórmulas matemáticas:** sintaxe LaTeX via `pymdownx.arithmatex`.

---

## 5. Ambiente Local e Validação

!!! warning "Estado atual (mutável)"
    O projeto usa `zensical==0.1.3` sobre Python `>= 3.12`. O `pyproject.toml` está compatível tanto com `python -m zensical` quanto com `uv run zensical`.

Execute os comandos na raiz de `platform-docs/`:

=== "Python"

    ```bash
    # Visualização local com live reload
    python -m zensical serve

    # Build estático limpo
    python -m zensical build --clean
    ```

=== "uv"

    ```bash
    # Visualização local com live reload
    uv run zensical serve

    # Build estático limpo
    uv run zensical build --clean
    ```

!!! info "Decisão"
    Nenhuma alteração de documentação deve ser commitada sem passar em `zensical build --clean` sem erros ou avisos de links/configuração.

---

## 6. Fluxo de Contribuição e Git

!!! info "Decisão"
    Toda contribuição segue os padrões de controle de versão do projeto:

    - **Commits atômicos e compiláveis:** cada commit representa uma única mudança coesa e deixa o site compilável por si só.
    - **Conventional Commits com contexto (em `pt-BR`):** use prefixos padrão (`docs:`, `chore:`, `fix:`, `feat:`) com **título e corpo em português do Brasil (`pt-BR`, com acentos)**, descrevendo **o que** mudou e **por quê**.
    - **Sem alterações permanentes/remotas sem autorização:** `git push`, tags, releases e exclusões destrutivas exigem aprovação explícita.

### Checklist antes do commit

- [ ] Texto direto, conciso, em `pt-BR` corretamente acentuado.
- [ ] Decisões e estados mutáveis explicitamente marcados.
- [ ] Novos arquivos registrados em `nav` no `zensical.toml`.
- [ ] `python -m zensical build --clean` executado sem erros.
- [ ] Nenhum arquivo de `site/` ou `.cache/` incluído no staging.
