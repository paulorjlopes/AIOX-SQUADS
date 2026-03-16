# GTM Tag — Gerenciar tags do GTM

Crie, edite, consulte ou remova tags no Google Tag Manager.

## Operações

### Ver tag
"mostre a tag {tag_id}" → `gtm_get_tag`

### Criar tag
"crie uma tag {tipo} chamada {nome}" → `gtm_create_tag`

Parâmetros obrigatórios:
- `account_id`, `container_id`, `workspace_id`
- `name` — nome da tag
- `type` — tipo da tag (exemplos abaixo)
- `parameter` — array de parâmetros da tag
- `firing_trigger_id` — array com IDs dos triggers

### Tipos de tag comuns

| Tipo | Descrição |
|------|-----------|
| `html` | HTML personalizado |
| `gaawc` | Google Analytics 4 (GA4) |
| `ua` | Universal Analytics (legado) |
| `awct` | Google Ads Conversion Tracking |
| `flc` | Floodlight Counter |
| `fls` | Floodlight Sales |
| `img` | Pixel de imagem |

### Atualizar tag
"atualize a tag {tag_id}" → `gtm_update_tag`

### Deletar tag
"delete a tag {tag_id}" → `gtm_delete_tag`

## Exemplo — criar tag GA4

```
name: "GA4 - Page View"
type: "gaawc"
parameter:
  - type: "template", key: "measurementId", value: "G-XXXXXXXXXX"
firing_trigger_id: ["2147479553"]  # All Pages trigger
```
