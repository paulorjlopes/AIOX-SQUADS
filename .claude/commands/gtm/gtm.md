# GTM — Google Tag Manager MCP

Use o MCP `gtm` para gerenciar o Google Tag Manager via API.

## Ferramentas disponíveis

| Ferramenta | Descrição |
|-----------|-----------|
| `gtm_list_accounts` | Lista todas as contas GTM acessíveis |
| `gtm_list_containers` | Lista containers de uma conta |
| `gtm_list_workspaces` | Lista workspaces de um container |
| `gtm_list_tags` | Lista todas as tags de um workspace |
| `gtm_get_tag` | Detalhes de uma tag específica |
| `gtm_create_tag` | Cria uma nova tag |
| `gtm_update_tag` | Atualiza uma tag existente |
| `gtm_delete_tag` | Remove uma tag |
| `gtm_list_triggers` | Lista todos os triggers |
| `gtm_list_variables` | Lista todas as variáveis |
| `gtm_create_version` | Cria uma nova versão do container |
| `gtm_publish_version` | Publica uma versão do container |
| `gtm_get_workspace_status` | Status do workspace (mudanças pendentes) |

## Hierarquia GTM

```
Conta (account_id)
└── Container (container_id)
    └── Workspace (workspace_id)
        ├── Tags
        ├── Triggers
        └── Variáveis
```

## Como usar

Sempre começe listando as contas:
1. `gtm_list_accounts` — obter account_id
2. `gtm_list_containers` — obter container_id
3. `gtm_list_workspaces` — obter workspace_id
4. Executar a operação desejada

## Exemplos de uso

- "liste todas as contas GTM"
- "quais containers tenho na conta X"
- "mostre as tags do workspace Y"
- "crie uma tag GA4 no container Z"
- "publique a versão mais recente"
