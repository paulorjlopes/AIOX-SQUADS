# Validate Tracking — Validação de Rastreamento End-to-End

ACTIVATION-NOTICE: Você está ativando o workflow de **Validação de Rastreamento**. Leia o agente em `squads/xquads-squads/traffic-masters/agents/pixel-specialist.md` e execute o workflow `squads/xquads-squads/traffic-masters/workflows/wf-validate-tracking.yaml` seguindo todas as fases.

## Workflow: wf-validate-tracking

**Agent:** Pixel Specialist (`pixel-specialist`)
**Squad:** Traffic Masters
**Task:** `squads/xquads-squads/traffic-masters/tasks/validate-tracking.md`
**Workflow:** `squads/xquads-squads/traffic-masters/workflows/wf-validate-tracking.yaml`
**Trigger:** `*validate-tracking`

## O que este workflow faz

Valida end-to-end se o rastreamento de uma página está funcionando:

| Fase | Check | Ferramentas |
|------|-------|-------------|
| 1 — Pixel Check | Pixel correto na conta Meta, last_fired_time, is_created_by_business | Meta Ads MCP |
| 2 — GTM Audit | Container live, tags com triggers, variáveis com IDs corretos | GTM API (service account) |
| 3 — Browser Inspect | GTM carrega, fbq inicializa, dataLayer ativo, WP Rocket blocking | Playwright |
| 4 — Conversion Test | Form submit → evento Lead dispara com nome correto | Playwright + Network |
| 5 — Fixes + Report | Correções automáticas via API, relatório final com status | GTM API + Meta MCP |

## Como usar

```
/traffic:validate-tracking
```

O agente vai solicitar:
- **URL da página** a validar
- **Plataformas** (meta, google, tiktok)
- **Alias da conta** de anúncios (opcional — ex: partners, saveco-educacao)
- **Página de conversão** / thank you (opcional)

## Activation Steps

1. Ler `squads/xquads-squads/traffic-masters/agents/pixel-specialist.md`
2. Adotar a persona Pixel Specialist
3. Coletar inputs do usuário (website, platform, account_alias, conversion_page)
4. Executar as 5 fases do workflow `wf-validate-tracking.yaml` em sequência
5. Emitir relatório final com status ✅/⚠️/❌ por check e ações corretivas

## Outputs esperados

```markdown
## Relatório de Validação de Tracking
Status Geral: ✅ OK | ⚠️ Parcial | ❌ Crítico

| Check | Status | Detalhe |
|-------|--------|---------|
| Pixel correto na conta | ✅ | ID: 684377252867531 |
| GTM com triggers | ✅ | v13 publicada |
| GTM carrega no browser | ✅ | hasGTM: true |
| FB Pixel inicializa | ✅ | hasFBQ: true |
| PageView dispara | ✅ | network confirmed |
| Lead event dispara | ✅ | standard/Lead |
| WP Rocket não bloqueia | ⚠️ | type=rocketlazyloadscript |

### Problemas Encontrados
...

### Ações Executadas
...

### Ações Pendentes
...
```

## Contexto do projeto

- **GTM Account:** 6313638523 (Save Company)
- **Service Account:** `tools/gtm-mcp/credentials/n8n-automacoes-439221-d1f8e533786b.json`
- **WordPress sites:** `tools/wordpress-mcp/wp-sites.json`
- **Meta accounts:** `tools/meta-ads-mcp/` (alias: partners, saveco-institucional, etc.)
- **Stape proxy pattern:** `api.{dominio}/dehjqkmnlstta.js`
