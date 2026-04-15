---
title: "Identifiers"
tags: [endereçamento, ID, estrutura, navegação, permanência]
created: 2026-04-15
updated: 2026-04-15
---

## Definição

Um **Identifier** (Identificador) é um **endereço único e permanente** para cada [[Zettel|Zettel]]. Sem identificadores, não é possível criar um [[Zettelkasten]] verdadeiro — você não conseguiria referenciar ou lincar notas.

---

## Por Que Identificadores São Críticos

### 1. Endereçamento Hipertextual

Para criar uma web de notas, você precisa poder **apontar para notas específicas**. Uma URL na internet aponta para uma página específica. Um identificador faz o mesmo em um Zettelkasten.

### 2. Permanência

O identificador **nunca muda**. Você pode renomear o título, editar o conteúdo, reorganizar a estrutura — mas o ID permanece idêntico. Isto garante que links antigos continuem válidos.

### 3. Agnticismo de Software

IDs baseados em padrões simples (timestamps, números) funcionam em **qualquer ferramenta**. Se você trocar de software, pode manter todos os IDs e links funcionando.

---

## Quatro Tipos de Identificadores

### 1. **Luhmann ID** (Hierárquico)

Formato: `1`, `1a`, `1a1`, `1a1a`, etc.

**Funcionamento**:
- Primeira nota: `1`
- Segunda nota sem relação: `2`
- Continuação/expansão de `1`: `1a`
- Continuação de `1a`: `1b`
- Comentário em `1a`: `1a1`

**Vantagens**:
- Reflete a hierarquia de ideias
- Excelente para papel (você sabe onde procurar fisicamente)

**Desvantagens**:
- Cumbersome digitalmente
- IDs podem ficar longos (`1a2b3c...`)
- Criação manual de números

### 2. **Time-Based ID** (Recomendado para Digital)

Formato: `202006110955` (YYYYMMDDHHMM)

Exemplo: 2020-06-11 às 09:55 → `202006110955`

**Vantagens**:
- Único por construção (nunca há colisão)
- Humanamente legível (você sabe quando foi criado)
- Gerado automaticamente
- Curto e simples
- Software-independent

**Desvantagens**:
- Nenhuma informação sobre relacionamento hierárquico (mas isso é bom para sistemas digitais)

### 3. **Arbitrary Unique String**

Números incrementais, strings aleatórias, UUIDs, hexadecimais, etc.

Exemplos: `42`, `abc123def`, `2F08729AEA` (timestamp em hex)

**Vantagens**:
- Podem ser muito curtos
- Flexível

**Desvantagens**:
- Perdem legibilidade
- Impossível criar manualmente
- Menos software-independent

### 4. **Title-Based ID** (Não Recomendado)

Usar o título do Zettel como seu ID.

**Problema crítico**:
Se você renomeia o Zetzel, todos os links quebram.

Mesmo que o software re-resolvendo os links (como alguns wikis fazem), você perde a independência de software.

---

## Recomendação de Sascha

**Para digital**: Use **time-based IDs**.

Propriedades:
- Permanentes
- Únicos
- Humanamente legíveis
- Software-independent
- Podem coexistir com full-text search como mecanismo de descoberta

---

## IDs e Full-Text Search

Em um Zettelkasten digital, você pode navegar de duas formas:

1. **Via ID direto**: Procura por `[[202006110955]]` para seguir um link
2. **Via full-text search**: Procura por uma palavra-chave para descobrir notas

Full-text search é tão poderoso quanto o register de Luhmann, mas mais flexível.

---

## Redundância Prática

O The Archive (software recomendado) coloca o ID em **dois lugares**:

1. No filename: `202006110955 - Atomicity.md`
2. No conteúdo: Na primeira linha do arquivo

Por quê? Portabilidade. Se você acessa via Dropbox (que só busca filenames), o ID ainda está no nome do arquivo.

---

## Relações Conceituais

- [[Zettels]] — unidades identificadas
- [[Link Context]] — ligações entre IDs
- [[Zettelkasten]] — sistema que depende de IDs para funcionar
