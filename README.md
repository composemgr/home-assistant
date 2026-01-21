# Home Assistant

A self-hosted home-assistant application.

## Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/home-assistant/main/docker-compose.yaml" | docker compose -f - up -d
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/home-assistant" ~/.local/srv/docker/home-assistant
cd ~/.local/srv/docker/home-assistant
docker compose up -d
```

### Option 3: Using composemgr
```bash
composemgr install home-assistant
```

## Configuration

See docker-compose.yaml for environment variables and configuration options.

## Documentation

Check the official project documentation for detailed setup and usage information.
