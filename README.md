## 👋 Welcome to home-assistant 🚀

Open source home automation platform

## 📋 Description

Home Assistant is a local-first home automation platform. It integrates with
thousands of devices and services — lights, sensors, locks, media players — and
automates them with rules, scenes, and scripts. All state stays on your host.

## 🚀 Services

- **app**: ghcr.io/home-assistant/home-assistant:latest

## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/home-assistant/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/home-assistant" ~/.local/srv/docker/home-assistant
cd ~/.local/srv/docker/home-assistant
cp default.env .env
docker compose --env-file .env up -d
```

### Option 3: Using composemgr
```bash
composemgr install home-assistant
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
```

Home Assistant is configured through its own web UI, not through environment
variables. Its `configuration.yaml` is written to
`volumes/config/home-assistant/configuration.yaml`.

See `docker-compose.yaml` for complete list of configurable options.

### Environment Files

`default.env.sample` holds the full set of variables and is copied to `.env`
before starting the stack:

```bash
cp default.env .env
docker compose --env-file .env up -d
```

`app.env.sample` holds the app-specific overrides and is copied to `app.env`:

```bash
cp app.env.sample app.env
```

`composemgr up` applies `app.env` and `default.env` automatically. Raw
`docker compose` commands need `--env-file .env` to pick up the same values.

### Reverse Proxy

Three standalone compose files ship in this repo:

| File | Use |
|------|-----|
| `docker-compose.yaml` | Default, published on `172.17.0.1:64199` |
| `docker-compose.traefik.yaml` | Behind an existing external `traefik` network |
| `docker-compose.tunnel.yaml` | Behind an existing external `cloudflare` tunnel network |

```bash
docker compose -f docker-compose.traefik.yaml --env-file .env up -d
```

## 🌐 Access

- **Web Interface**: http://172.17.0.1:64199

## 📂 Volumes

- `./volumes/config/home-assistant` - Configuration, state database, and media
- `/etc/localtime` - Host timezone
- `/run/dbus` - Host D-Bus, for device discovery
- `/dev/bus/usb` - Host USB bus, for Zigbee/Z-Wave sticks

## 🔐 Security

- Change all default passwords before deploying to production
- The container runs `privileged` so that hardware discovery works — only run
  it on a host you control
- Home Assistant is published on the Docker host gateway only; do not expose it
  directly to the internet
- Configure HTTPS using a reverse proxy (nginx, traefik, caddy)
- Regularly update Docker images for security patches
- Backup your data regularly

## 🔍 Logging

```shell
docker compose --env-file .env logs -f app
```

## 🛠️ Management

```bash
# Start services
docker compose --env-file .env up -d

# Stop services
docker compose --env-file .env down

# Update to latest images
docker compose --env-file .env pull && docker compose --env-file .env up -d

# View logs
docker compose --env-file .env logs -f

# Restart services
docker compose --env-file .env restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
