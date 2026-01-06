# n8n Docker Setup

This repository contains a Docker Compose configuration for running n8n locally.

## Prerequisites

- Docker
- Docker Compose

## Configuration

Before starting n8n, update the timezone settings in `docker-compose.yml`:

```yaml
environment:
  - GENERIC_TIMEZONE=America/New_York  # Change to your timezone
  - TZ=America/New_York                # Change to your timezone
```

Find your timezone from the [TZ database](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones).

## Usage

### Start n8n

```bash
docker compose up -d
```

This will:

- Create the `n8n_data` volume for persistent storage
- Start the n8n container in detached mode
- Make n8n available at <http://localhost:5678>

### View Logs

```bash
# Follow logs in real-time
docker compose logs -f

# View last 100 lines
docker compose logs --tail=100
```

### Stop n8n

```bash
docker compose down
```

### Restart n8n

```bash
docker compose restart
```

### Stop and Remove Data

```bash
# Warning: This will delete all your workflows and data
docker compose down -v
```

## Accessing n8n

Once running, open your browser and navigate to:

```
http://localhost:5678
```

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
