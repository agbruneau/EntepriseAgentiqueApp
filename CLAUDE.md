# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**"L'Entreprise Agentique"** — a French-language monograph (81 chapters, 5 volumes) on enterprise transformation toward agentic architectures. **This is a publishing project, not a software codebase.** Content is Markdown; the PDF pipeline converts Markdown → Typst → PDF.

**Authoritative editorial reference:** `INSTRUCTION.MD` (in French, contains full per-volume directives, complete terminology glossary, and detailed quality checklists).

## Repository Structure

```
Volume_I_Fondations_Entreprise_Agentique/   (28 ch. — Theoretical foundations)
Volume_II_Infrastructure_Agentique/          (15 ch. — Confluent + Google Cloud)
Volume_III_Apache_Kafka_Guide_Architecte/    (12 ch. — Kafka deep-dive)
Volume_IV_Apache_Iceberg_Lakehouse/          (16 + 2 ch. — Data Lakehouse)
Volume_V_Developpeur_Renaissance/            (10 ch. — Human capital & skills)
pdf-generator/                               (Pandoc + Typst PDF pipeline)
```

- Each volume: `README.md` + `Introduction_*/` + `Partie_*/Chapitre_*/` with `.md` files
- Root files: `INSTRUCTION.MD` (editorial rules), `TOC.md` (detailed TOC), `README.md` (navigation)

## PDF Generation

Prerequisites: Python 3.10+, Pandoc 3.0+, Typst 0.11+, `pip install pypdf pyyaml`

```bash
python pdf-generator/scripts/generate.py --volume IV           # Single volume
python pdf-generator/scripts/generate.py --volume all          # All sequential
python pdf-generator/scripts/generate.py --volume all --parallel  # All parallel
python pdf-generator/scripts/generate.py --consolidated        # Merged monograph
python pdf-generator/scripts/validate.py --volume all          # Validate sources
```

Pipeline: `.md` files → concatenated → Pandoc + Lua filters (`callouts.lua`, `figures.lua`, `cross-refs.lua`) → `.typ` → Typst → PDF. Output: `pdf-generator/output/{volumes,consolidated}/`.

## File Naming

- Chapters: `Chapitre_[VOL]_[N].md` (e.g. `Chapitre_I_1.md`, `Chapitre_IV_16.md`) — no description in filename
- Introductions: `Introduction.md` per volume
- Annexes (Vol. IV): `Annexe_IV_A.md`, `Annexe_IV_B.md`
- Directories keep full descriptive names

## Editorial Standards

### Language

- **Quebec professional French** (infonuagique, courriel…) — avoid untranslated anglicisms except recognized technical terms
- Prefer **fluid prose** over bullet lists
- First acronym occurrence: full form + (acronym); then acronym only
- Audience: enterprise architects, CTOs, transformation consultants

### Per-Volume Style

| Vol. | Tone | Theory/Practice | Focus |
|------|------|-----------------|-------|
| I | Academic-professional | 60/40 | Strategic perspective, decision-makers |
| II | Technical-practical | 40/60 | Implementation, engineering teams |
| III | Technical-architectural | 50/50 | Architect trade-offs, justifications |
| IV | Technical-architectural | 45/55 | Data engineering, performance, costs |
| V | Philosophical-professional | 70/30 | Humanist, reflective, inspiring |

### Mandatory Terminology (Lexique Obligatoire)

| Term | Usage |
|------|-------|
| Entreprise agentique | NOT "entreprise IA" / "entreprise intelligente" |
| Agents cognitifs | NOT "agents IA" alone |
| Maillage agentique / Agentic Mesh | Multi-agent orchestration |
| Système nerveux numérique | Event infrastructure metaphor |
| Interopérabilité Cognitivo-Adaptative (ICA) | AI-enhanced semantic understanding |
| Architecture réactive | Event-driven architecture |
| Backbone événementiel | Event backbone infrastructure |
| Lakehouse / Data Lakehouse | NOT "data lake" alone |
| Contrats de données | Contractual schemas between systems |
| Constitution agentique | Agent governance rules |
| AgentOps | Agent operations discipline |
| Architecte d'intentions | Intention Architect role |
| Berger d'intention | Intention Shepherd role |
| Jumeau Numérique Cognitif (JNC) | AI representation of an entity |
| Saga chorégraphiée | Distributed transactions via events |
| CQRS / Event Sourcing / Outbox transactionnel | Architectural patterns |
| A2A / MCP / AsyncAPI | Agent & async interoperability protocols |
| Développeur Renaissance | Modern polymath profile (Vol. V) |
| Les Cinq Piliers | Curiosité, Pensée systémique, Communication, Ownership, Interdisciplinarité |
| Spécification-Driven Development (SDD) | Development methodology (Vol. V) |

### Chapter Format

- **10,000 words** target per chapter
- Structure: Introduction (10-15%) → Development (75-80%) → Conclusion (10%)
- Each chapter ends with a structured **Résumé** section + Tableau Récapitulatif
- Each chapter must be **independently comprehensible** while maintaining cross-chapter coherence
- Citations: 2023-2026 sources preferred; format `Name (Year)` or `"selon [Org, Year]"`; leaders: Confluent, Apache, Google Cloud, Anthropic, Dremio, Microsoft

## Normalized Markdown Structure

**Section numbering prefixes:** `I.N`, `II.N`, `III.N`, `IV.N`, `V.N`

### Chapter Template

```markdown
# Chapitre [VOL].[NUM] — [Titre]

> *« Citation optionnelle »*
> — Auteur

---

## [VOL].[NUM].0 Introduction
[150-300 mots]

## [VOL].[NUM].1 [Section principale]
### [VOL].[NUM].1.1 [Sous-section]

...

## [VOL].[NUM].[N] Conclusion
[150-200 mots]

## [VOL].[NUM].[N+1] Résumé
Ce chapitre a exploré [thème]. Points essentiels :
**[Concept]** : [2-3 phrases]

### Tableau Récapitulatif
| Concept | Définition | Implication |
|---------|------------|-------------|

*Chapitre suivant : Chapitre [VOL].[NUM+1] — [Titre]*
```

Last chapter of a volume ends with: `*Fin du Volume [N] — [Titre]*`

### Title Hierarchy

| Level | Usage | Example |
|-------|-------|---------|
| `#` H1 | Chapter title only | `# Chapitre I.5 — Écosystème API` |
| `##` H2 | Main sections | `## I.5.1 L'API comme Interface Stratégique` |
| `###` H3 | Subsections | `### I.5.1.1 Patterns RESTful` |
| `####` H4 | Detail points (rare, unnumbered) | |

### Callouts (Blockquote Format)

**Universal (all volumes):** `> **Définition formelle**`, `> **Perspective stratégique**`, `> **Exemple concret**`

**Technical (Vol. II-IV):** with structured fields `*Contexte/Défi/Solution/Leçon*`

| Callout | Volumes | Fields |
|---------|---------|--------|
| **Note de terrain** | II-IV | Contexte, Défi, Solution, Leçon |
| **Décision architecturale** | II-IV | Contexte, Analyse, Décision, Justification |
| **Anti-patron** | II-IV | Error description + alternative |
| **Étude de cas : [Nom]** | IV | Secteur, Défi, Solution, Résultats |
| **Migration : [Titre]** | IV | De, Vers, Stratégie, Résultats |
| **Performance : [Titre]** | IV | Metrics and benchmarks |
| **Figure historique : [Nom]** | V | Époque, Domaines, Contribution, Leçon |
| **Réflexion** | V | Question for introspection |
| **Manifeste** | V | Guiding principle |

All callouts use blockquote syntax: `> **Label**` followed by `>` content lines.

## Technology Stack (Subject Matter)

- **Apache Kafka / Confluent Platform** — Event backbone (Streams, ksqlDB, Connect, Schema Registry)
- **Google Cloud Vertex AI** — Cognitive layer (Agent Builder, Model Garden, RAG)
- **Apache Iceberg** — Data Lakehouse (Dremio, Trino, Spark as query engines)
- **Microsoft Fabric / OneLake / Power BI Direct Lake** — Data platform integration
- **A2A, MCP, AsyncAPI** — Agent & async interoperability protocols
- **OpenTelemetry** — Observability standard

## Cross-Volume References

Use these French patterns when referencing other volumes:

| Pattern | Target |
|---------|--------|
| "comme défini au Volume I…" | Conceptual foundations |
| "voir Volume II pour l'implémentation…" | Confluent + GCP implementation |
| "le Volume III approfondit…" | Kafka architecture details |
| "le Volume IV détaille…" | Data lakehouse patterns |
| "le Volume V explore…" | Human skills & practices |
