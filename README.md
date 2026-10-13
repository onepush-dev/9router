# 9Router — multi-provider LLM router with a web UI. Deploy on Railway with one click.

[![Deploy on Railway](https://railway.app/button.svg)](https://railway.app/new/template/TEMPLATE_CODE)

Self-hosted [9Router](https://github.com/decolua/9router) (decolua/9router `0.5.95`) — route LLM traffic across providers, manage API keys, and use the built-in dashboard. Zero deploy-time config: secrets are generated automatically.

## Services
| Service | Source | Notes |
|---|---|---|
| 9router | `decolua/9router:0.5.95@sha256:4316fefb95ea642d57db885d906b1227b1768b15ac5def314621fd781da7b3f1` | web + API on port `20128`; volume `/app/data` |

## Variables (9router)
| Variable | Template value | Secret |
|---|---|---|
| PORT | `20128` | |
| HOSTNAME | `0.0.0.0` | |
| DATA_DIR | `/app/data` | |
| BASE_URL | `https://${{RAILWAY_PUBLIC_DOMAIN}}` | |
| NEXT_PUBLIC_BASE_URL | `https://${{RAILWAY_PUBLIC_DOMAIN}}` | |
| CLOUD_URL | `https://9router.com` | |
| INITIAL_PASSWORD | `${{secret(24, alphanumeric)}}` | yes |
| JWT_SECRET | `${{secret(64, alphanumeric)}}` | yes |
| API_KEY_SECRET | `${{secret(48, alphanumeric)}}` | yes |
| MACHINE_ID_SALT | `${{secret(32, alphanumeric)}}` | yes |
| AUTH_COOKIE_SECURE | `true` | |
| ENABLE_REQUEST_LOGS | `false` | |
| REQUIRE_API_KEY | `true` | |
| HEADROOM_URL | _(empty)_ | optional |
| SEARXNG_URL | _(empty)_ | optional |
| RAILWAY_DEPLOYMENT_DRAINING_SECONDS | `30` | |

## Notes
- Healthcheck: `/api/health` (timeout 300s). Restart policy: `ON_FAILURE`.
- Persistent data lives on the volume at `/app/data` (`DATA_DIR`).
- After deploy, open the public URL and sign in with the generated `INITIAL_PASSWORD` (Variables tab).
- Image is pinned by digest so marketplace deploys stay reproducible.
- Upstream: https://github.com/decolua/9router · Docker Hub: `decolua/9router`
