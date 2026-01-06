# n8n AI Demo

This repository contains materials for the 3rd and final class for the ImprovingU workshop "Automate Your World with AI Agents". This class focuses on a hands-on exploration of n8n AI capabilities.

## About the Workshop

Join us for an exciting three-session workshop where we'll dive into the world of AI agents and collaboratively build real world agents from the ground up! In this hands-on series, attendees will work together to define the agent's features and functionality, leveraging the power of cutting-edge agent builders to transform ideas into a working agents in real time. No prior AI expertise is required and you don't need to be a developer; just bring your creativity and enthusiasm for innovation as we explore the future of automation together!

## Repository Contents

- Docker Compose configuration for running n8n locally
- Presentation materials (Slidev-based slides)
- Workshop examples and demonstrations

## Prerequisites

Before the workshop, please ensure you have the following configured:

### Google Gemini API Key (Free Tier)

1. Visit [Google AI Studio](https://aistudio.google.com/app/apikey)
2. Sign in with your Google account
3. Click "Create API Key"
4. Copy and save your API key securely

### Docker

**macOS:**

- Download [Docker Desktop for Mac](https://www.docker.com/products/docker-desktop/)
- Install and launch Docker Desktop

**Windows:**

- Download [Docker Desktop for Windows](https://www.docker.com/products/docker-desktop/)
- Install and launch Docker Desktop

**Linux:**

- Follow the [official Docker installation guide](https://docs.docker.com/engine/install/) for your distribution

### n8n

n8n will run via Docker using the configuration in this repository. No separate installation required - just follow the setup instructions below.

#### Configuration

Before starting n8n, update the timezone settings in `docker-compose.yml`:

```yaml
environment:
  - GENERIC_TIMEZONE=America/New_York  # Change to your timezone
  - TZ=America/New_York                # Change to your timezone
```

Find your timezone from the [TZ database](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones).

#### Usage

##### Start n8n

```bash
docker compose up -d
```

This will:

- Create the `n8n_data` volume for persistent storage
- Start the n8n container in detached mode
- Make n8n available at <http://localhost:5678>

##### View Logs

```bash
# Follow logs in real-time
docker compose logs -f

# View last 100 lines
docker compose logs --tail=100
```

##### Stop n8n

```bash
docker compose down
```

##### Restart n8n

```bash
docker compose restart
```

##### Stop and Remove Data

```bash
# Warning: This will delete all your workflows and data
docker compose down -v
```

#### Accessing n8n

Once running, open your browser and navigate to:

```text
http://localhost:5678
```

## Presentation

The presentation is built with [Slidev](https://sli.dev/) and uses the Improving-25 theme.

### Running the Presentation

```bash
cd presentation
pnpm install
pnpm dev
```

The presentation will be available at <http://localhost:3030/>

## Data Persistence

All n8n data (workflows, credentials, settings) is stored in the `n8n_data` Docker volume, which persists between container restarts.

## Environment Variables

The following environment variables are configured:

- `GENERIC_TIMEZONE`: Sets the timezone for n8n
- `TZ`: Sets the system timezone
- `N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS`: Enforces proper file permissions
- `N8N_RUNNERS_ENABLED`: Enables n8n runners for task execution

## Troubleshooting

### Port Already in Use

If port 5678 is already in use, modify the port mapping in `docker-compose.yml`:

```yaml
ports:
  - "8080:5678"  # Use port 8080 instead
```

### Permission Issues

If you encounter permission issues with the volume, try:

```bash
docker compose down
docker volume rm n8n_data
docker compose up -d
```

## Additional Resources

- [n8n Documentation](https://docs.n8n.io/)
- [n8n Community Forum](https://community.n8n.io/)
