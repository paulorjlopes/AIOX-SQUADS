# AIOS Forge Squad — Ecosystem Status

**Última verificação:** 2026-03-11T18:59:28Z
**Próximo ciclo recomendado:** 2026-04-11

---

## Claude Code

| Item | Status | Versão / Detalhe |
|------|--------|------------------|
| Claude Code CLI | STABLE | v2.1.73 (latest) |
| Skills System | STABLE | Substitui `.claude/commands/` |
| Custom Subagents | STABLE | v2.1.63+ com `memory:`, `isolation:` |
| Hooks System | STABLE | HTTP hooks + novos eventos |
| MCP Tool Search | STABLE | `ENABLE_TOOL_SEARCH=auto` |
| Auto-Memory | STABLE | MEMORY.md 200 linhas |
| Agent Teams | EXPERIMENTAL | `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1` |

## Modelos Claude

| Modelo | Status |
|--------|--------|
| claude-opus-4-6 | LATEST |
| claude-sonnet-4-6 | LATEST |
| claude-haiku-4-5-20251001 | STABLE |
| claude-3-haiku-20240307 | DEPRECATED (remover antes 19/04/2026) |
| claude-opus-4 / claude-opus-4-1 | REMOVED do Claude Code |

## MCP Protocol

| Item | Status | Notas |
|------|--------|-------|
| HTTP streamable transport | STABLE | Padrão recomendado |
| SSE transport | DEPRECATED | Migrar para HTTP |
| Dynamic tool updates (`list_changed`) | STABLE | — |
| OAuth 2.0 | STABLE | v2.1.64+ com `authServerMetadataUrl` |
| Plugin-provided MCP Servers | STABLE | `.mcp.json` inline em `plugin.json` |

## AIOS Framework

| Item | Status | Notas |
|------|--------|-------|
| AIOX v5.0.3 | STABLE | Versão em uso |
| Forge Squad v1.0.2 | STABLE | Knowledge base inicializada |
| xquads-squads | STABLE | 13 squads integrados |
