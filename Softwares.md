docker stop open-webui
docker rm -f open-webui


# open-webui & Ollama

```
docker run -d \
-p 127.0.0.1:3000:8080 \
-p 127.0.0.1:11434:11434 \
--gpus=all \
-e OLLAMA_HOST=0.0.0.0 \
-v ollama:/root/.ollama \
-v open-webui:/app/backend/data \
--name open-webui \
--restart always \
ghcr.io/open-webui/open-webui:ollama
```

# abogen for audiobook

Update docker-compose to support GPU
```
-        TORCH_INDEX_URL: ${TORCH_INDEX_URL:-https://download.pytorch.org/whl/cu126}
+        TORCH_INDEX_URL: ${TORCH_INDEX_URL:-https://download.pytorch.org/whl/cu128}
```



```
sudo chown -R $USER:$USER data/
sudo chmod -R 775

docker compose up -d --build
```

# Openclaw

```
docker ps 
CONTAINER ID   IMAGE                                  COMMAND                  CREATED         STATUS                    PORTS                                                                                          NAMES
cadef06a2c88   openclaw:local                         "node dist/index.js …"   2 minutes ago   Up 2 minutes                                                                                                             openclaw-openclaw-cli-run-e462989eeaa6
79fec1564e87   ghcr.io/open-webui/open-webui:ollama   "bash start.sh"          9 hours ago     Up 43 minutes (healthy)   0.0.0.0:11434->11434/tcp, [::]:11434->11434/tcp, 0.0.0.0:3000->8080/tcp, [::]:3000->8080/tcp   open-webui
```


docker network connect openclaw_default open-webui

```
git clone https://github.com/openclaw/openclaw
./docker-setup.sh
◇  I understand this is personal-by-default and shared/multi-user use requires lock-down. Continue?
│  Yes
│
◇  Onboarding mode
│  Manual
│
◇  What do you want to set up?
│  Local gateway (this machine)
│
◇  Workspace directory
│  /home/node/.openclaw/workspace
│
◇  Model/auth provider
│  Custom Provider
|
◇  Endpoint compatibility
│  OpenAI-compatible
│
◇  API Base URL
│  http://open-webui:11434/v1
│
◇  How do you want to provide this API key?
│  Paste API key now
│
◇  API Key (leave blank if not required)
│
│
◇  Model ID
│  llama3.1:8b
│
◇  Verification successful.
│
◆  Endpoint ID
│  custom-open-webui-11434█





◇  Dashboard ready ────────────────────────────────────────────────────────────────╮
│                                                                                  │
│  Dashboard link (with token):                                                    │
│  http://127.0.0.1:18789/#token=af49f27d9dcf4099127b84cf8f409cd34d59c0e0075658a9  │
│  Copy/paste this URL in a browser on this machine to control OpenClaw.           │
│  No GUI detected. Open from your computer:                                       │
│  ssh -N -L 18789:127.0.0.1:18789 user@<host>                                     │
│  Then open:                                                                      │
│  http://localhost:18789/                                                         │
│  http://localhost:18789/#token=af49f27d9dcf4099127b84cf8f409cd34d59c0e0075658a9  │
│  Docs:                                                                           │
│  https://docs.openclaw.ai/gateway/remote                                         │
│  https://docs.openclaw.ai/web/control-ui                                         │
│                                                                                  │
├──────────────────────────────────────────────────────────────────────────────────╯
│
◇  Web search (optional) ─────────────────────────────────────────────────────────────────╮
│                                                                                         │
│  If you want your agent to be able to search the web, you’ll need an API key.           │
│                                                                                         │
│  OpenClaw uses Brave Search for the `web_search` tool. Without a Brave Search API key,  │
│  web search won’t work.                                                                 │
│                                                                                         │
│  Set it up interactively:                                                               │
│  - Run: openclaw configure --section web                                                │
│  - Enable web_search and paste your Brave Search API key                                │
│                                                                                         │
│  Alternative: set BRAVE_API_KEY in the Gateway environment (no config changes).         │
│  Docs: https://docs.openclaw.ai/tools/web                                               │
│                                                                                         │
├─────────────────────────────────────────────────────────────────────────────────────────╯
│
◇  What now ─────────────────────────────────────────────────────────────╮
│                                                                        │
│  What now: https://openclaw.ai/showcase ("What People Are Building").  │
│                                                                        │
├────────────────────────────────────────────────────────────────────────╯
│
└  Onboarding complete. Use the dashboard link above to control OpenClaw.


==> Control UI origin allowlist
WARN[0000] The "CLAUDE_AI_SESSION_KEY" variable is not set. Defaulting to a blank string. 
WARN[0000] The "CLAUDE_WEB_SESSION_KEY" variable is not set. Defaulting to a blank string. 
WARN[0000] The "CLAUDE_WEB_COOKIE" variable is not set. Defaulting to a blank string. 
WARN[0000] The "CLAUDE_AI_SESSION_KEY" variable is not set. Defaulting to a blank string. 
WARN[0000] The "CLAUDE_WEB_SESSION_KEY" variable is not set. Defaulting to a blank string. 
WARN[0000] The "CLAUDE_WEB_COOKIE" variable is not set. Defaulting to a blank string. 
 Container openclaw-openclaw-cli-run-fb8829eba471 Creating 
 Container openclaw-openclaw-cli-run-fb8829eba471 Created 
Config overwrite: /home/node/.openclaw/openclaw.json (sha256 952004730fd75fc58a51db4e3e1e15f4977a94c1974797b6dc61fa6e5a12c3da -> 0318ecf75bb026b057bb0721893861af919b6ee476d8468e60437161d4342117, backup=/home/node/.openclaw/openclaw.json.bak)
Set gateway.controlUi.allowedOrigins to ["http://127.0.0.1:18789"] for non-loopback bind.

==> Provider setup (optional)
WhatsApp (QR):
  docker compose -f /home/hamid/repositories/openclaw/docker-compose.yml run --rm openclaw-cli channels login
Telegram (bot token):
  docker compose -f /home/hamid/repositories/openclaw/docker-compose.yml run --rm openclaw-cli channels add --channel telegram --token <token>
Discord (bot token):
  docker compose -f /home/hamid/repositories/openclaw/docker-compose.yml run --rm openclaw-cli channels add --channel discord --token <token>
Docs: https://docs.openclaw.ai/channels

==> Starting gateway
WARN[0000] The "CLAUDE_AI_SESSION_KEY" variable is not set. Defaulting to a blank string. 
WARN[0000] The "CLAUDE_WEB_SESSION_KEY" variable is not set. Defaulting to a blank string. 
WARN[0000] The "CLAUDE_WEB_COOKIE" variable is not set. Defaulting to a blank string. 
WARN[0000] The "CLAUDE_AI_SESSION_KEY" variable is not set. Defaulting to a blank string. 
WARN[0000] The "CLAUDE_WEB_SESSION_KEY" variable is not set. Defaulting to a blank string. 
WARN[0000] The "CLAUDE_WEB_COOKIE" variable is not set. Defaulting to a blank string. 
[+] up 1/1
 ✔ Container openclaw-openclaw-gateway-1 Started                                                                                                                                                                                          0.3s

Gateway running with host port mapping.
Access from tailnet devices via the host's tailnet IP.
Config: /home/hamid/.openclaw
Workspace: /home/hamid/.openclaw/workspace
Token: b56f7f76adbc7055c04ab7713f31d52f90a9e9582645f3fe2dcb9335b1064e57

Commands:
  docker compose -f /home/hamid/repositories/openclaw/docker-compose.yml logs -f openclaw-gateway
  docker compose -f /home/hamid/repositories/openclaw/docker-compose.yml exec openclaw-gateway node dist/index.js health --token "b56f7f76adbc7055c04ab7713f31d52f90a9e9582645f3fe2dcb9335b1064e57"
```




# aider

```
docker pull paulgauthier/aider-full
docker run -it --user $(id -u):$(id -g) --volume $(pwd):/app paulgauthier/aider-full 


docker run -it \
  --user $(id -u):$(id -g) \
  --volume $(pwd):/app \
  --add-host=host.docker.internal:host-gateway \
  -e OLLAMA_API_BASE=http://host.docker.internal:11434 \
  paulgauthier/aider-full \
  --model ollama_chat/qwen2.5-coder:7b
```
