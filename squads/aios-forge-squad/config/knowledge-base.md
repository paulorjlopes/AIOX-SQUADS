# AIOS Forge Squad — Knowledge Base

## Última Atualização
- **Data:** 2026-03-11T18:59:28Z
- **Fonte:** Self-update pipeline (Scout → Oracle → Forge → Sentinel)
- **Checado por:** Hermes (aios-scout)
- **Scope:** all (Claude Code + AIOS ecosystem)

---

## Claude Code — Estado Atual

- **Versão:** v2.1.73 (latest em 2026-03-11)
- **Última verificação:** 2026-03-11
- **Modelos padrão no Claude Code:** claude-sonnet-4-6 (Sonnet), claude-opus-4-6 (Opus)

### Features Relevantes para AIOS

| Feature | Status | Notas |
|---------|--------|-------|
| Custom Agents via `.claude/agents/` | STABLE | Suporta `memory:`, `isolation: worktree`, `skills:`, `hooks:` |
| Skills via `.claude/skills/` | STABLE | Substitui `.claude/commands/` — migração recomendada |
| Rules via `.claude/rules/` | STABLE | Suporte a `paths:` frontmatter para carregamento contextual |
| Hooks (command, HTTP, prompt) | STABLE | Novos eventos: `InstructionsLoaded`, `SubagentStart/Stop`, `WorktreeCreate/Remove` |
| Memory — Auto-Memory (MEMORY.md) | STABLE | Linhas 1-200 carregadas; tópicos em arquivos separados |
| MCP — Tool Search (Lazy Loading) | STABLE | `ENABLE_TOOL_SEARCH=auto`; redução de até 95% de tokens |
| Agent Teams | EXPERIMENTAL | `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1`; 3-5 teammates ideal |
| `.claude/teams/` e Permissions | STABLE | Roles, `allowedMcpServers`, `deny: ["Agent(...)"]` |

---

## Modelos Claude — Estado Atual (2026-03-11)

| Modelo | API ID | Contexto | Max Output | Status |
|--------|--------|----------|------------|--------|
| Claude Opus 4.6 | `claude-opus-4-6` | 200K / 1M (beta) | 128K | LATEST — Padrão recomendado |
| Claude Sonnet 4.6 | `claude-sonnet-4-6` | 200K / 1M (beta) | 64K | LATEST — Default Claude Code |
| Claude Haiku 4.5 | `claude-haiku-4-5-20251001` | 200K | 64K | STABLE |
| Claude Haiku 3 | `claude-3-haiku-20240307` | — | — | DEPRECATED — Remover antes de 19/04/2026 |

**1M Token Context (beta):** disponível para Opus 4.6 e Sonnet 4.6 via header `context-1m-2025-08-07`.

---

## Skills System — Padrão Atual

O sistema de Skills substituiu o sistema legado de Slash Commands (`.claude/commands/`).

### Estrutura de uma Skill
```
.claude/skills/<skill-name>/
├── SKILL.md           # Arquivo principal (obrigatório)
├── template.md        # Templates auxiliares (opcional)
├── examples/          # Exemplos de saída esperada (opcional)
└── scripts/           # Scripts executáveis (opcional)
```

### Frontmatter do SKILL.md — Campos Completos
```yaml
name: skill-name
description: "Descrição usada por Claude para auto-invocação"
disable-model-invocation: true   # só usuário pode invocar
user-invocable: false            # só Claude pode invocar
allowed-tools: [Read, Grep]      # ferramentas sem aprovação
model: sonnet                    # modelo específico
context: fork                    # executa em subagente isolado
agent: Explore                   # tipo de subagente
hooks:                           # hooks scoped à skill
argument-hint: "<args>"          # hint no autocomplete
```

### Skills Bundled Nativas
| Skill | Descrição |
|-------|-----------|
| `/simplify` | Review de código em 3 agentes paralelos (reuso, qualidade, eficiência) |
| `/batch` | Paralelismo massivo — decompõe em 5-30 unidades em git worktrees |
| `/debug` | Analisa session debug log |
| `/loop [interval]` | Executa prompts em intervalos recorrentes |
| `/claude-api` | Carrega referência completa da Claude API |

---

## Custom Subagents — Padrão Atual

Definidos em `.claude/agents/` (projeto) ou `~/.claude/agents/` (global).

### Frontmatter Completo de Subagente
```yaml
name: agent-name
description: "Quando usar este agente"
tools: [Read, Grep, Bash]
disallowedTools: [Write]
model: sonnet
permissionMode: default          # default | acceptEdits | dontAsk | bypassPermissions | plan
maxTurns: 20
skills: [skill-name]
mcpServers: [mcp-name]
hooks:
  SubagentStop:
    - command: "cleanup.sh"
memory: user                     # user | project | local
background: true                 # sempre como background task
isolation: worktree              # git worktree isolado
```

### Memória Persistente de Subagentes
```
~/.claude/agent-memory/<name>/
├── MEMORY.md          # Primeiras 200 linhas carregadas
├── debugging.md       # Notas específicas
└── patterns.md        # Padrões descobertos
```

### Built-in Subagents
| ID | Modelo | Ferramentas | Uso |
|----|--------|-------------|-----|
| `Explore` | Haiku | Somente leitura | Busca e análise de codebase |
| `Plan` | Herda | Somente leitura | Pesquisa em plan mode |
| `general-purpose` | Herda | Todas | Tarefas complexas |

**Nota:** O tool `Task` foi renomeado para `Agent` (v2.1.63). `Task(...)` ainda funciona como alias.

---

## Hooks System — Padrão Atual

### Tipos de Hooks
| Tipo | Descrição |
|------|-----------|
| `command` | Shell script executado localmente |
| `http` | POST JSON para URL, recebe JSON de volta (v2.1.63+) |
| `prompt` | Executa prompt LLM como hook |

### Eventos Disponíveis
| Evento | Contexto | Notas |
|--------|----------|-------|
| `PreToolUse` | Antes de tool call | Exit code 2 = bloqueio garantido |
| `PostToolUse` | Após tool call | — |
| `Stop` | Ao finalizar resposta | — |
| `SubagentStart` | Início de subagente | `agent_id`, `agent_type` no payload |
| `SubagentStop` | Fim de subagente | — |
| `InstructionsLoaded` | CLAUDE.md / rules carregados | Útil para auditoria |
| `WorktreeCreate` | Criação de worktree | `worktree` no payload |
| `WorktreeRemove` | Remoção de worktree | — |
| `TeammateIdle` | Teammate ocioso (Agent Teams) | Exit code 2 = manter trabalhando |
| `TaskCompleted` | Task concluída (Agent Teams) | Exit code 2 = bloquear marcação |

### Payload Novos Campos (2025+)
- `agent_id`: ID do subagente
- `agent_type`: tipo do subagente
- `worktree`: `{name, path, branch, original_repo}`

---

## MCP Integration — Estado Atual

### MCP Tool Search (Lazy Loading)
- **Ativação:** `ENABLE_TOOL_SEARCH=auto` (padrão quando > 10% da janela)
- **Modos:** `auto`, `auto:<N>%`, `true`, `false`
- **Redução:** até 95% de tokens
- **Requisito:** Sonnet 4+ ou Opus 4+ (Haiku não suporta)

### Escopos Renomeados
| Novo | Antigo | Descrição |
|------|--------|-----------|
| `project` | `local` | Privado ao projeto atual |
| `user` | `global` | Disponível em todos os projetos |

### SSE Deprecado
Migrar MCP servers de SSE para HTTP streamable transport.

### Permissões em `.mcp.json`
- `--scope project` para servidores compartilhados (commitar `.mcp.json`)
- `allowedMcpServers` para allowlist de servidores por agente

---

## Memory System — Estado Atual

### Auto-Memory
- Storage: `~/.claude/projects/<project>/memory/MEMORY.md`
- **Limite:** Primeiras 200 linhas carregadas — manter conciso
- Tecla `#` para adicionar memories rapidamente ao CLAUDE.md
- Toggle: `/memory` ou `autoMemoryEnabled: false` nas settings

### CLAUDE.md — Boas Práticas
- HTML comments no CLAUDE.md ficam ocultos para Claude (visíveis ao Read tool)
- `--add-dir`: CLAUDE.md de diretórios adicionais NÃO carregados por padrão
  - Ativar: `CLAUDE_CODE_ADDITIONAL_DIRECTORIES_CLAUDE_MD=1`
- Managed policy locations (IT/DevOps):
  - macOS: `/Library/Application Support/ClaudeCode/CLAUDE.md`
  - Linux/WSL: `/etc/claude-code/CLAUDE.md`
  - Windows: `C:\Program Files\ClaudeCode\CLAUDE.md`

### Rules — `.claude/rules/`
- Frontmatter `paths:` para carregamento contextual por arquivo
- Suporte a symlinks no diretório `.claude/rules/`
- User-level rules: `~/.claude/rules/` (cross-project, não commitadas)

---

## Agent Teams — Estado Atual (Experimental)

- **Ativação:** `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1`
- **Arquitetura:** Team Lead + Teammates com task list compartilhada
- **Task storage:** `~/.claude/tasks/{team-name}/`
- **Display modes:** `in-process` (Shift+Down para navegar) | `tmux` | `iTerm2`
- **Dimensionamento ideal:** 3-5 teammates, 5-6 tasks por teammate
- **Limitações:** Sem `/resume` para in-process, sem times aninhados, VS Code Terminal não suporta split panes

---

## Ecossistema MCP — Estado Atual

- **Docker MCP Toolkit:** Ativo, `docker-gateway` para servidores dentro de Docker
- **MCP servers configurados:** EXA (web search), Context7 (docs), Apify (scraping)
- **Secrets Bug:** Contornar editando `~/.docker/mcp/catalogs/docker-mcp.yaml` diretamente
- **Plugin-provided MCP Servers:** Plugins podem empacotar servidores MCP em `.mcp.json`

---

## Ações — Status Atualizado (2026-03-12)

| # | Ação | Impacto | Urgência | Status |
|---|------|---------|----------|--------|
| 1a | Skills: Adicionar `name:` + `description:` nos 7 agentes `afs/` | CRITICAL | Alta | ✅ RESOLVIDO (2026-03-12) |
| 1b | Skills: Migrar 26 agentes `AIOX/` para `.claude/skills/` | CRITICAL | Baixa | 🔵 DECISÃO ESTRATÉGICA — ambos coexistem; migração completa requer epic dedicado |
| 2 | Haiku 3 deprecado — nenhum uso real encontrado no projeto | HIGH | Alta | ✅ RESOLVIDO — nenhuma referência ativa encontrada |
| 3 | MEMORY.md — 63 linhas, abaixo do limite de 200 | HIGH | Média | ✅ RESOLVIDO — já OK |
| 4 | Configurar `ENABLE_TOOL_SEARCH=auto` para MCP | HIGH | Média | PENDENTE |
| 5 | Avaliar Custom Subagents com `memory: user` para agentes AIOS | HIGH | Média | PENDENTE |
| 6 | Migrar MCP servers SSE → HTTP transport | MEDIUM | Média | PENDENTE |
| 7 | Avaliar Agent Teams para workflows de review paralelo | MEDIUM | Baixa | PENDENTE |

### Nota Estratégica — Skills Migration AIOX Agents

Os 26 arquivos em `.claude/commands/AIOX/` são agentes complexos com YAML inline (não frontmatter). A migração completa para o formato Skills requer:
- Refatoração de cada agente para usar YAML frontmatter
- Criação de estrutura `.claude/skills/AIOX/` espelhando a atual
- Teste de regressão de todos os slash commands

**Decisão:** Manter em `.claude/commands/` — ambos os sistemas coexistem e funcionam. Migração completa é um epic separado quando houver benefício claro (ex.: auto-invocação necessária para agentes AIOX).
