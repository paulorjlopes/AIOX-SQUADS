# AIOS Forge Squad — Update Log

## 2026-03-11T18:59:28Z — Self-Update (Initial)

- **Scope:** all (Claude Code + AIOS ecosystem)
- **Sources checked:** 18 fontes verificadas
- **Updates found:** 9 findings
- **Critical updates:** 2 (Skills migration, Haiku 3 deprecation)
- **High updates:** 5 (Subagents, Hooks, MCP, Memory, Modelos)
- **Medium updates:** 2 (Agent Teams, Enterprise)
- **Ações requeridas:** 7

### Updates Encontrados

1. **Skills System** (CRITICAL) — `.claude/commands/` → `.claude/skills/` migration necessária
2. **Haiku 3 Deprecado** (HIGH) — `claude-3-haiku-20240307` removido em 19/04/2026 → migrar para `claude-haiku-4-5-20251001`
3. **Custom Subagents** (HIGH) — novos campos: `memory:`, `isolation: worktree`, `background:`, `skills:`, `hooks:`
4. **Hooks Expandidos** (HIGH) — HTTP hooks, `InstructionsLoaded`, `SubagentStart/Stop`, `WorktreeCreate/Remove`
5. **MCP Tool Search** (HIGH) — Lazy loading com `ENABLE_TOOL_SEARCH=auto`; SSE deprecado
6. **Auto-Memory** (HIGH) — MEMORY.md limite 200 linhas; tecla `#` para memories rápidas
7. **Modelos Claude 4.6** (HIGH) — `claude-opus-4-6` e `claude-sonnet-4-6` são os latest; Opus 4/4.1 removidos
8. **Agent Teams** (MEDIUM) — Experimental; `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1`
9. **Enterprise Governance** (MEDIUM) — Managed MCP, `pluginTrustMessage`, audit logs

### Artefatos Criados/Atualizados
- `config/knowledge-base.md` — CRIADO (knowledge base inicial)
- `config/last-check.json` — CRIADO (timestamp do check)
- `config/update-log.md` — CRIADO (este arquivo)
- `config/ecosystem-status.md` — CRIADO (status do ecossistema)

---

## 2026-03-12 — Resolução de Ações Urgentes

- **Executor:** Oracle → Catalyst + Forge → Sentinel
- **Ações resolvidas:** 3 de 7

### ✅ Ação 1a — Skills System: `name:` + `description:` nos agentes afs/

Adicionado `name:` e `description:` no YAML frontmatter dos 7 agentes do Forge Squad:
- `.claude/commands/afs/agents/aios-oracle.md`
- `.claude/commands/afs/agents/aios-scout.md`
- `.claude/commands/afs/agents/aios-architect.md`
- `.claude/commands/afs/agents/aios-catalyst.md`
- `.claude/commands/afs/agents/aios-forge.md`
- `.claude/commands/afs/agents/aios-nexus.md`
- `.claude/commands/afs/agents/aios-sentinel.md`

**Resultado:** Todos os agentes afs/ agora aparecem com descrição completa na lista de skills do Claude Code, habilitando auto-invocação.

### ✅ Ação 2 — Haiku 3 Deprecado

Verificação completa: nenhum arquivo do projeto usa `claude-3-haiku-20240307` como modelo ativo. Ação encerrada sem mudanças necessárias.

### ✅ Ação 3 — MEMORY.md

MEMORY.md tem 63 linhas — abaixo do limite de 200. Ação encerrada sem mudanças necessárias.

### 🔵 Decisão Estratégica — Migração Completa `AIOX/` agents

Os 26 agentes em `.claude/commands/AIOX/` usam YAML inline (não frontmatter). Migração completa para `.claude/skills/` requer epic dedicado. Ambos os sistemas coexistem — nenhum impacto funcional.
