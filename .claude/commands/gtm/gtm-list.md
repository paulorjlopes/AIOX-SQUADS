# GTM List — Listar recursos do GTM

Liste contas, containers, workspaces, tags, triggers e variáveis do Google Tag Manager.

## Uso

Informe o que deseja listar:

- **Contas:** "liste as contas GTM" → `gtm_list_accounts`
- **Containers:** "liste os containers da conta {account_id}" → `gtm_list_containers`
- **Workspaces:** "liste os workspaces do container {container_id}" → `gtm_list_workspaces`
- **Tags:** "liste as tags do workspace {workspace_id}" → `gtm_list_tags`
- **Triggers:** "liste os triggers do workspace {workspace_id}" → `gtm_list_triggers`
- **Variáveis:** "liste as variáveis do workspace {workspace_id}" → `gtm_list_variables`
- **Status:** "status do workspace {workspace_id}" → `gtm_get_workspace_status`

## Fluxo padrão (quando IDs não são conhecidos)

1. `gtm_list_accounts` → escolher conta
2. `gtm_list_containers` → escolher container
3. `gtm_list_workspaces` → escolher workspace
4. Listar o recurso desejado

Se os IDs já forem fornecidos, pule direto para o passo necessário.
