# GTM Publish — Versionar e publicar container GTM

Crie versões e publique containers no Google Tag Manager.

## Fluxo recomendado

1. Verificar mudanças pendentes → `gtm_get_workspace_status`
2. Criar versão → `gtm_create_version`
3. Publicar versão → `gtm_publish_version`

## Operações

### Ver mudanças pendentes
"qual é o status do workspace?" → `gtm_get_workspace_status`

Retorna todas as mudanças não publicadas (tags, triggers, variáveis adicionadas/editadas/removidas).

### Criar versão
"crie uma versão chamada {nome}" → `gtm_create_version`

Parâmetros:
- `account_id`, `container_id`, `workspace_id` (obrigatórios)
- `name` — nome da versão (ex: "v1.2 - GA4 + Meta Pixel")
- `notes` — notas descritivas (opcional)

### Publicar versão
"publique a versão {version_id}" → `gtm_publish_version`

Parâmetros:
- `account_id`, `container_id`, `version_id`

## Boas práticas

- Sempre verificar o status antes de criar uma versão
- Nomear versões de forma descritiva (ex: "2026-03 - Pixel Meta + GA4 Events")
- Adicionar notas com o contexto das mudanças
- Criar a versão ANTES de publicar (são dois passos separados)
