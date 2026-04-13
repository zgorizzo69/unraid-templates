# hermes-agent

Unraid template for running [Hermes Agent](https://hermes-agent.nousresearch.com/) in Docker.

## What this template does

- Uses image: `nousresearch/hermes-agent:latest`
- Persists Hermes state in `/opt/data` (mapped to `/mnt/user/appdata/hermes-agent` by default)
- Starts in persistent gateway mode by default with `gateway run`
- Adds `--shm-size=1g` in Extra Parameters for better browser automation stability
- Enables Hermes API server by default for Open WebUI (`API_SERVER_ENABLED=true`)

## First-time setup (important)

Before running persistent gateway mode, initialize Hermes once to create config files and `.env`:

1. Open the container in Unraid and set **Post Arguments** to `setup`
2. Start the container and complete the setup wizard
3. Stop the container
4. Set **Post Arguments** back to `gateway run`
5. Start the container again

This follows the official Docker flow from Hermes docs.

## Open WebUI out-of-the-box setup

This template is preconfigured so Open WebUI can connect immediately.

1. In Unraid Hermes template, set **API server key** (`API_SERVER_KEY`) to a strong secret.
2. Deploy Hermes container.
3. Deploy Open WebUI with:
   - `OPENAI_API_BASE_URL=http://<UNRAID_IP>:8642/v1`
   - `OPENAI_API_KEY=<same API_SERVER_KEY value>`
4. Open Open WebUI and select the `hermes-agent` model.

If Open WebUI runs as another Docker container on the same Unraid host, use the host IP (or `host.docker.internal` with host-gateway mapping).

## Notes

- Do **not** run multiple Hermes containers against the same `/opt/data` directory.
- API keys can be stored in `/opt/data/.env` (recommended) or passed as env vars.
- Port `8642` is published by default for Open WebUI integration.
- Telegram allowlist is supported via `TELEGRAM_ALLOWED_USERS` (comma-separated numeric IDs).
- Common LLM provider keys are available in the template advanced fields (`OPENROUTER_API_KEY`, `OPENAI_API_KEY`, `ANTHROPIC_API_KEY`, and additional provider keys from Hermes docs).
- Official references:
  - `https://hermes-agent.nousresearch.com/docs/reference/environment-variables`
  - `https://hermes-agent.nousresearch.com/docs/user-guide/messaging/telegram`

# COMMAND

```bash
/usr/local/emhttp/plugins/dynamix.docker.manager/scripts/docker create --name='hermes-agent' --net='bridge' --restart='unless-stopped' --shm-size='1g' -e 'API_SERVER_ENABLED'='true' -e 'API_SERVER_HOST'='0.0.0.0' -e 'API_SERVER_PORT'='8642' -e 'API_SERVER_KEY'='change-me' -e 'TELEGRAM_BOT_TOKEN'='' -e 'TELEGRAM_ALLOWED_USERS'='' -e 'OPENROUTER_API_KEY'='' -e 'OPENAI_API_KEY'='' -e 'ANTHROPIC_API_KEY'='' -e 'AI_GATEWAY_API_KEY'='' -e 'GLM_API_KEY'='' -e 'KIMI_API_KEY'='' -e 'MINIMAX_API_KEY'='' -e 'MINIMAX_CN_API_KEY'='' -e 'KILOCODE_API_KEY'='' -e 'XIAOMI_API_KEY'='' -e 'HF_TOKEN'='' -e 'GOOGLE_API_KEY'='' -e 'DASHSCOPE_API_KEY'='' -e 'DEEPSEEK_API_KEY'='' -e 'OPENCODE_ZEN_API_KEY'='' -e 'OPENCODE_GO_API_KEY'='' -p '8642:8642/tcp' -v '/mnt/user/appdata/hermes-agent':'/opt/data':'rw' 'nousresearch/hermes-agent:latest' gateway run
```
