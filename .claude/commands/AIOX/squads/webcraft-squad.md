# WebCraft Squad

ACTIVATION-NOTICE: You are activating the **WebCraft Squad**. Read the complete entry agent definition at `squads/xquads-squads/webcraft-squad/agents/webcraft-chief.md` and follow ALL activation instructions in that file exactly. Do not improvise or skip any steps.

## Squad: WebCraft Squad

**Location:** `squads/xquads-squads/webcraft-squad/`
**Entry Agent:** `webcraft-chief` (Web Intelligence Commander — Orchestrator)
**Slash Command:** `/AIOX:squads:webcraft-squad`
**Version:** 2.0.0 (merged with design-squad)
**Description:** Squad unificado de Web Excellence — 14 experts + 3 especialistas + 1 orquestrador. Cobertura completa: análise de websites, design criativo, design systems (Atomic Design), UX/UI, DesignOps, animações, design tokens, performance, acessibilidade, SEO e GEO.

## Activation Steps

1. Read `squads/xquads-squads/webcraft-squad/agents/webcraft-chief.md` fully
2. Adopt the WebCraft Chief persona defined in that file
3. Follow the agent's activation-instructions exactly
4. Display the squad greeting and await user input

## Available Agents

### Tier 0 — Orchestration
| Agent | Expertise | File |
|-------|-----------|------|
| WebCraft Chief | Orchestrator | `agents/webcraft-chief.md` |

### Tier 1 — Web Analysis, Creative & Visibility
| Agent | Expertise | File |
|-------|-----------|------|
| Vitaly Friedman | Website Analysis & Patterns | `agents/vitaly-friedman.md` |
| Tobias van Schneider | Creative Direction & Anti-Generic Design | `agents/tobias-van-schneider.md` |
| Val Head | Web Animation & Motion Design | `agents/val-head.md` |
| Jina Anne | Design Tokens & Tokenization | `agents/jina-anne.md` |
| Addy Osmani | Performance & Core Web Vitals | `agents/addy-osmani.md` |
| Heydon Pickering | Accessibility & Inclusive Design | `agents/heydon-pickering.md` |
| Lily Ray | SEO Strategy & E-E-A-T | `agents/lily-ray.md` |
| Fabrice Canel | GEO & AI Search Visibility | `agents/fabrice-canel.md` |

### Tier 1 — Design Systems & Operations (merged from design-squad)
| Agent | Expertise | File |
|-------|-----------|------|
| Brad Frost | Atomic Design & Design Systems | `agents/brad-frost.md` |
| Dan Mall | Design at Scale & Creative Direction | `agents/dan-mall.md` |
| Dave Malouf | DesignOps & Design Leadership | `agents/dave-malouf.md` |

### Tier 2 — Design Specialists (merged from design-squad)
| Agent | Expertise | File |
|-------|-----------|------|
| UX Designer | User Research & Interaction Design | `agents/ux-designer.md` |
| UI Engineer | Frontend Implementation & Production Code | `agents/ui-engineer.md` |
| Visual Generator | Visual Assets & AI Image Prompts | `agents/visual-generator.md` |

## Available Tasks

### Web Analysis & Audits
- `*dissect {url}` — Complete multi-dimensional website analysis
- `*audit-performance {url}` — Core Web Vitals & performance audit
- `*audit-a11y {url}` — WCAG 2.2 accessibility audit
- `*audit-seo {url}` — Technical SEO & E-E-A-T audit
- `*audit-geo {url}` — AI search visibility & GEO audit
- `*search {url}` — Complete search visibility audit (SEO + GEO)

### Design & Creation
- `*design` — Create original, anti-generic web design
- `*tokenize` — Design token architecture creation
- `*create-design-system` — Build complete atomic design system
- `*create-component-spec` — Component specification with variants, tokens, a11y
- `*design-ux-flow` — UX research, personas, wireframes, usability testing

### Operations & Handoff
- `*setup-design-ops` — Establish DesignOps practice
- `*audit-design` — Design maturity assessment (3 lenses)
- `*generate-handoff` — Developer handoff documentation
- `*review` — Quality review and synthesis of deliverables

## Available Workflows

### Original WebCraft Workflows
- `wf-site-dissection.yaml` — Full 8-dimension site analysis (structure, visual, motion, tokens, performance, a11y, SEO, GEO)
- `wf-design-creation.yaml` — Design creation from brief to delivery (research, creative, motion, tokens, validation)
- `wf-search-audit.yaml` — Complete search visibility audit (CWV, a11y, SEO, GEO)

### Design System Workflows (merged from design-squad)
- `wf-design-system-creation.yaml` — Full design system build (audit → tokens → components → governance → launch)
- `wf-feature-design.yaml` — Feature design process (research → wireframes → visual → handoff → integration)

## Routing Domains

| Domain | Primary Agent | Secondary Agent |
|--------|--------------|-----------------|
| Website Analysis | vitaly-friedman | addy-osmani |
| Creative Design | tobias-van-schneider | val-head |
| Animation & Motion | val-head | tobias-van-schneider |
| Design Tokens | jina-anne | brad-frost |
| Performance | addy-osmani | vitaly-friedman |
| Accessibility | heydon-pickering | ux-designer |
| SEO | lily-ray | fabrice-canel |
| GEO / AI Search | fabrice-canel | lily-ray |
| Design Systems | brad-frost | dan-mall |
| Design at Scale | dan-mall | dave-malouf |
| DesignOps | dave-malouf | dan-mall |
| UX Research | ux-designer | vitaly-friedman |
| UI Implementation | ui-engineer | brad-frost |
| Visual Assets | visual-generator | tobias-van-schneider |
| Component Spec | brad-frost | ui-engineer |
