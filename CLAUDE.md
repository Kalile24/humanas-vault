# CLAUDE.md — Humanas Vault: Wiki Operating Manual

> Read this file at the start of every session. It defines the schema, conventions, and workflows for this LLM-maintained knowledge base.

---

## 2.1 Project Overview

**Vault:** `humanas-vault`
**Domínios:** Filosofia · História · Teologia · Literatura

Este vault segue o padrão Karpathy: arquivos brutos em `raw/` (gerenciado pelo humano), wiki estruturada em `wiki/` (mantida pelo Claude). O humano coleta e cura; o Claude resume, interliga e mantém.

Sources típicos: clippings de artigos, excertos de livros, textos patrísticos, papers de filosofia e história, transcrições de aulas.

---

## 2.2 Directory Conventions

```
/
├── raw/               ← domínio do humano. NUNCA modificar.
│   ├── assets/        ← imagens referenciadas por documentos raw
│   └── repos/         ← snapshots de repositórios (raro neste vault)
├── wiki/
│   ├── sources/       ← uma página de resumo por documento ingerido
│   ├── concepts/      ← artigos temáticos sintetizados
│   ├── entities/      ← pessoas, obras, movimentos, lugares
│   ├── outputs/       ← resultados de queries arquivados
│   └── assets/        ← imagens geradas ou referenciadas pelo wiki
├── tools/
├── CLAUDE.md
├── wiki/index.md
└── wiki/log.md
```

**Regras:**
- `raw/` é **read-only** para o Claude.
- Nomes de arquivo: minúsculas, hífens, `.md`. Ex: `suma-teologica-i.md`.
- **Toda página wiki deve ter YAML frontmatter:**

```yaml
---
title: "Título da Página"
tags: [tag1, tag2]
created: YYYY-MM-DD
updated: YYYY-MM-DD
source_count: N
---
```

Páginas de source usam `source_file` em vez de `source_count`:

```yaml
---
title: "Source: Título do Documento"
tags: [tag1, tag2]
created: YYYY-MM-DD
updated: YYYY-MM-DD
source_file: raw/filename.ext
---
```

---

## 2.3 Ingest Workflow

Execute **um source por vez** por padrão.

1. Ler o arquivo em `raw/`.
2. Discutir os 3–5 principais takeaways antes de escrever qualquer coisa.
3. Criar página de resumo em `wiki/sources/`.
4. Identificar e atualizar páginas de conceitos e entidades afetadas.
5. Se não existir página relevante, criar.
6. Atualizar `wiki/index.md`.
7. Append em `wiki/log.md`: `## [YYYY-MM-DD] ingest | <Título do Source>`
8. Reportar resumo: quais arquivos foram criados/atualizados.

---

## 2.4 Query Workflow

1. Ler `wiki/index.md` para identificar páginas relevantes.
2. Ler essas páginas na íntegra.
3. Sintetizar resposta com citações inline como links markdown relativos.
4. Perguntar se o humano quer arquivar o resultado em `wiki/outputs/`.
5. Se sim: criar página e atualizar index e log.

Log: `## [YYYY-MM-DD] query | <Título ou Pergunta>`

**Formatos disponíveis:** narrativa markdown · tabela comparativa · síntese em bullets · slide deck Marp (`marp: true` no frontmatter).

---

## 2.5 Lint Workflow

Passes: contradiction check · staleness check · orphan check · stub check · missing concept check · gap suggestions.

Log: `## [YYYY-MM-DD] lint | Health check`

---

## 2.6 Index Conventions (`wiki/index.md`)

Organizado por categoria: **Sources · Concepts · Entities · Outputs**.

```markdown
- [Título](categoria/arquivo.md) — descrição em uma linha
```

Atualizar em **toda** operação de ingest, query-filing ou update.

---

## 2.7 Log Conventions (`wiki/log.md`)

- Append-only. Nunca editar entradas passadas.
- Formato: `## [YYYY-MM-DD] <operação> | <título>`
- 2–4 linhas descrevendo o que aconteceu.
- Operações válidas: `setup` · `ingest` · `query` · `lint` · `update`

---

## 2.8 Princípios Gerais

- Prefira atualizar páginas existentes a criar novas.
- Toda página nova deve ter ao menos um backlink antes do fim da sessão.
- Sinalize incerteza: *"Esta afirmação aparece em [Fonte X](../sources/x.md) mas não é corroborada em outras fontes."*
- Ao criar entidade ou conceito, escanear páginas existentes por menções e adicionar links.

---

## 2.9 Tipos de Source

| Tipo | source_type | Campos obrigatórios |
|------|-------------|---------------------|
| Web clipping | `clipping` | title, author, url, ingested, tags |
| Paper | `paper` | title, author, url, published, venue, ingested, tags |
| Livro/capítulo | `book-excerpt` | title, author, published, pages, ingested, tags |
| Vídeo/podcast | `video` / `podcast` | title, author, url, ingested, tags |

---

## 2.10 Taxonomia de Tags

Use **2–6 tags** por página. Sempre ao menos 1 tag de domínio + 1 de subtópico.

### Filosofia
`filosofia-clássica` · `filosofia-medieval` · `escolástica` · `filosofia-moderna` · `filosofia-contemporânea` · `ética` · `estética` · `metafísica` · `epistemologia` · `filosofia-da-mente` · `fenomenologia` · `lógica` · `bem` · `verdade` · `beleza` · `transcendência` · `ontologia` · `antropologia-filosófica`

### Teologia
`teologia` · `teologia-natural` · `teologia-dogmática` · `teologia-moral` · `sagrada-escritura` · `patrística` · `escolástica` · `mística` · `liturgia` · `eclesiologia` · `cristologia` · `apologética`

### História
`história-antiga` · `história-medieval` · `história-moderna` · `história-contemporânea` · `história-da-filosofia` · `história-da-igreja` · `história-da-ciência` · `biografia`

### Literatura
`literatura` · `poesia` · `romance` · `ensaio` · `retórica` · `hermenêutica` · `crítica-literária` · `narrativa`

### Pontes entre domínios
`filosofia-e-teologia` · `história-da-filosofia` · `filosofia-medieval` · `ética-e-política` · `estética-e-literatura`
