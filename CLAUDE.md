# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is **"L'Entreprise Agentique"** (The Agentic Enterprise), a French-language academic/professional monograph exploring enterprise transformation toward agentic architectures. The project consists of **81 chapters across 5 volumes** covering theoretical foundations, technical implementations, and strategic implications.

**This is a publishing project, not a software codebase.** Content is authored in Markdown (.md) format. The PDF generation pipeline converts Markdown → Typst → PDF.

## Repository Structure

```
Volume_I_Fondations_Entreprise_Agentique/   (28 chapters - Theoretical foundations)
Volume_II_Infrastructure_Agentique/          (15 chapters - Confluent + Google Cloud)
Volume_III_Apache_Kafka_Guide_Architecte/    (12 chapters - Kafka deep-dive)
Volume_IV_Apache_Iceberg_Lakehouse/          (16 + 2 chapters - Data Lakehouse)
Volume_V_Developpeur_Renaissance/            (10 chapters - Human capital & skills)
pdf-generator/                               (PDF generation toolchain)
```

Each volume contains:
- `README.md` - Volume overview and navigation
- `Partie_*/Chapitre_*/` - Individual chapter directories with .md files
- `Introduction_*/` - Volume introduction directory

**Root-level files:**
- `INSTRUCTION.MD` - Consolidated editorial guidelines for all volumes (in French, authoritative source)
- `CLAUDE.md` - Claude Code configuration (this file, in English)
- `TOC.md` - Full table of contents with section-level detail
- `README.md` - Project overview with chapter navigation links

## PDF Generation Commands

The `pdf-generator/` directory contains a Pandoc + Typst pipeline. Prerequisites: Python 3.10+, Pandoc 3.0+, Typst 0.11+, and `pip install pypdf pyyaml`.

```bash
# Generate a single volume PDF
python pdf-generator/scripts/generate.py --volume IV

# Generate all volumes sequentially
python pdf-generator/scripts/generate.py --volume all

# Generate all volumes in parallel
python pdf-generator/scripts/generate.py --volume all --parallel

# Generate consolidated monograph (all 5 volumes merged)
python pdf-generator/scripts/generate.py --consolidated

# Validate source files before generation
python pdf-generator/scripts/validate.py --volume all
python pdf-generator/scripts/validate.py --volume III --verbose
```

Pipeline: Markdown files → concatenated per volume → Pandoc converts to Typst (with Lua filters for callouts, figures, cross-refs) → Typst compiles to PDF. Output goes to `pdf-generator/output/volumes/` and `pdf-generator/output/consolidated/`.

## File Naming Conventions

**Markdown chapter files**: `Chapitre_[VOL]_[numéro].md` (e.g., `Chapitre_I_1.md`, `Chapitre_IV_16.md`)

- Volume prefix is Roman numeral (I, II, III, IV, V)
- Underscore separates volume number from chapter number
- No textual description in filename
- Introductions: `Introduction.md` in each volume
- Annexes (Volume IV): `Annexe_IV_A.md`, `Annexe_IV_B.md`
- Directories retain their full descriptive names

## Editorial Standards

### Language & Terminology

- **Quebec professional French** (infonuagique, courriel, etc.) — avoid untranslated anglicisms except recognized technical terms
- Prefer **fluid prose** over bullet lists
- First acronym occurrence: full form followed by acronym in parentheses; subsequent uses: acronym only
- Target audience: Enterprise architects, CTOs, transformation consultants

### Per-Volume Style & Balance

| Volume | Tone | Theory/Practice | Structure Notes |
|--------|------|-----------------|-----------------|
| I | Academic-professional | 60/40 | Strategic perspective for decision-makers |
| II | Technical-practical | 40/60 | Implementation-oriented for engineering teams |
| III | Technical-architectural | 50/50 | Architect's perspective: trade-offs, justifications |
| IV | Technical-architectural | 45/55 | Data engineering: performance, costs, governance |
| V | Philosophical-professional | 70/30 | Humanist, reflective, inspiring tone |

### Mandatory Terminology (Lexique Obligatoire)

**Core Concepts:**

| Term | Usage |
|------|-------|
| Entreprise agentique | NOT "entreprise IA" or "entreprise intelligente" |
| Agents cognitifs | NOT "agents IA" alone |
| Maillage agentique / Agentic Mesh | Multi-agent orchestration |
| Système nerveux numérique | Event infrastructure metaphor |
| Interopérabilité Cognitivo-Adaptative (ICA) | AI-enhanced semantic understanding |

**Architecture & Infrastructure:**

| Term | Usage |
|------|-------|
| Architecture réactive | Event-driven architecture |
| Backbone événementiel | Event backbone infrastructure |
| Lakehouse / Data Lakehouse | Unified architecture (NOT "data lake" alone) |
| Contrats de données | Contractual schemas between systems |

**Governance & Operations:**

| Term | Usage |
|------|-------|
| Constitution agentique | Agent governance rules |
| AgentOps | Agent operations discipline |
| Architecte d'intentions | Intention Architect role |
| Berger d'intention | Intention Shepherd role |
| Jumeau Numérique Cognitif (JNC) | AI representation of an entity |

**Patterns & Protocols:**

| Term | Usage |
|------|-------|
| Saga chorégraphiée | Distributed transactions via events |
| CQRS | Command/query separation |
| Event Sourcing | Event-based persistence |
| Outbox transactionnel | Publication guarantee pattern |
| A2A (Agent-to-Agent) | Inter-agent communication protocol |
| MCP (Model Context Protocol) | Model context protocol |
| AsyncAPI | Async API specification |

**Volume V Specific:**

| Term | Usage |
|------|-------|
| Développeur Renaissance | Modern polymath profile |
| Les Cinq Piliers | Curiosité appliquée, Pensée systémique, Communication précise, Ownership, Interdisciplinarité |
| Spécification-Driven Development (SDD) | Development methodology |

### Chapter Format

- **Target length**: 10,000 words per chapter
- **Structure**: Introduction (10-15%) → Development (75-80%) → Conclusion/Transition (10%)
- **Output format**: Markdown (.md)
- **Each chapter ends with**: Structured "Résumé" section
- **Each chapter must be comprehensible independently** while maintaining cross-chapter coherence

### Citation Convention

- Prioritize 2023-2026 technical sources
- Reference leaders: Confluent, Apache, Google Cloud, Anthropic, Dremio, Microsoft
- Format: Name (Year) or "selon [Organization, Year]"
- Prefer primary sources (official documentation, research papers)

---

## Normalized Markdown Structure

All chapter markdown files follow this standardized structure for PDF consolidation.

### Chapter Header (Obligatoire)

```markdown
# Chapitre [VOL].[NUM] — [Titre du Chapitre]

> *« Citation inspirante optionnelle »*
> — Auteur

---

## [VOL].[NUM].0 Introduction

[Paragraphe contextuel 150-300 mots...]
```

**Volume prefixes:**
- Volume I: `I.N`
- Volume II: `II.N`
- Volume III: `III.N`
- Volume IV: `IV.N`
- Volume V: `V.N`

### Title Hierarchy

| Level | Syntax | Usage | Example |
|-------|--------|-------|---------|
| H1 `#` | Chapter title only | `# Chapitre I.5 — Écosystème API` |
| H2 `##` | Main sections | `## I.5.1 L'API comme Interface Stratégique` |
| H3 `###` | Subsections | `### I.5.1.1 Patterns RESTful` |
| H4 `####` | Detail points (rare) | Not numbered |

### Callouts (Blockquote Format)

**Universal callouts (all volumes):**

```markdown
> **Définition formelle**
>
> [Term defined and concise explanation]

> **Perspective stratégique**
>
> [Business implications, recommendations]

> **Exemple concret**
>
> [Practical illustration with context]
```

**Technical callouts (Volumes II-IV):**

```markdown
> **Note de terrain**
>
> *Contexte* : [Description]
> *Défi* : [Problem]
> *Solution* : [Approach]
> *Leçon* : [Lesson learned]

> **Décision architecturale**
>
> *Contexte* : [Situation]
> *Analyse* : [Options]
> *Décision* : [Choice]
> *Justification* : [Reasons]

> **Anti-patron**
>
> *[Error description]* : [Explanation and alternative]

> **Étude de cas : [Name]**
>
> *Secteur* : [Industry]
> *Défi* : [Challenge]
> *Solution* : [Architecture]
> *Résultats* : [Metrics]

> **Migration : [Title]**
>
> *De* : [Source state]
> *Vers* : [Target state]
> *Stratégie* : [Approach]
> *Résultats* : [Outcomes]

> **Performance : [Title]**
>
> [Performance metrics and benchmarks]
```

**Volume V callouts:**

```markdown
> **Figure historique : [Nom]**
>
> *Époque* : [Period]
> *Domaines* : [Disciplines mastered]
> *Contribution* : [Major contribution]
> *Leçon pour aujourd'hui* : [Applicable teaching]

> **Réflexion**
>
> [Question inviting professional introspection]

> **Manifeste**
>
> [Guiding principle of the Développeur Renaissance]
```

### Chapter End Structure

```markdown
---

## [VOL].[NUM].[N] Conclusion

[Synthesis 150-200 words]

---

## [VOL].[NUM].[N+1] Résumé

Ce chapitre a exploré [theme]. Points essentiels :

**[Concept 1]** : [Summary 2-3 sentences]

**[Concept 2]** : [Summary 2-3 sentences]

### Tableau Récapitulatif

| Concept | Définition | Implication |
|---------|------------|-------------|
| [Term] | [Definition] | [Application] |

---

*Chapitre suivant : Chapitre [VOL].[NUM+1] — [Title]*
```

**For volume final chapters:**
```markdown
*Fin du Volume [N] — [Volume Title]*
```

## Technology Stack (Subject Matter)

The monograph covers these technologies:
- **Apache Kafka / Confluent Platform** - Event backbone (Kafka Streams, ksqlDB, Kafka Connect, Schema Registry)
- **Google Cloud Vertex AI** - Cognitive layer (Agent Builder, Model Garden, RAG)
- **Apache Iceberg** - Data Lakehouse (with Dremio, Trino, Apache Spark as query engines)
- **Microsoft Fabric / OneLake / Power BI Direct Lake** - Data platform integration
- **AsyncAPI** - Asynchronous protocol specification
- **A2A, MCP** - Agent interoperability protocols
- **OpenTelemetry** - Observability standard

## Cross-Volume References

When writing content, use these patterns:
- "comme défini au Volume I..." → Conceptual foundations
- "voir Volume II pour l'implémentation..." → Technical implementation (Confluent + GCP)
- "le Volume III approfondit..." → Kafka architecture details
- "le Volume IV détaille..." → Data lakehouse patterns
- "le Volume V explore..." → Human skills and development practices
