# Midocu CLI

**Enterprise installer for Midocu CRM platform**

## Quick Start

### 1. Download & Install

```bash
# Linux (recommended)
sudo curl -L -o /usr/local/bin/midocu https://github.com/oxsbilisim/midocu-cli-releases/releases/latest/download/midocu-linux
sudo chmod +x /usr/local/bin/midocu
```

### 2. Install Midocu CRM

```bash
midocu install
```

Follow the interactive prompts to enter:
- License key (provided by Midocu team)
- Server hostname/IP
- Database URL
- Redis URL

### 3. Verify Installation

```bash
midocu status
```

## Commands

### Service Management

```bash
midocu install          # Install Midocu CRM stack
midocu status           # Check service status
midocu logs             # View all logs
midocu logs backend     # View backend logs only
midocu update           # Update to latest version
midocu restart          # Restart all services
midocu stop             # Stop all services
midocu start            # Start all services
midocu uninstall        # Remove all containers
midocu uninstall -r     # Remove containers AND CLI binary
```

### Admin Management

```bash
# Create initial admin (first-time setup)
midocu init-admin --from-container

# List all admins
midocu list-admins --from-container

# Reset admin password
midocu reset-password --from-container
```

**Note:** Use `--from-container` to auto-detect database URL from running container.

## Services

After installation, the following services will be available:

| Service | Port | URL |
|---------|------|-----|
| CRM Backend | 8001 | `http://your-server:8001` |
| CRM Dashboard | 3001 | `http://your-server:3001` |
| Field Agent App | 3002 | `http://your-server:3002` |

## Requirements

- **Docker** 20.10 or later
- **Linux** Ubuntu 20.04+, Debian 11+, RHEL 8+
- **RAM** Minimum 2GB
- **Disk** Minimum 10GB free space

### Network Requirements

Ensure your server can access:
- `docker.io` - Docker Hub (for pulling images)
- `api.midocu.ai` - License validation
- `github.com` - CLI updates

## Troubleshooting

### Service not starting

```bash
# Check logs
midocu logs backend

# Restart services
midocu restart
```

### Database connection issues

```bash
# Verify database is accessible
midocu logs backend | grep -i database

# Check environment
docker exec midocu-backend env | grep DATABASE
```

### License validation failed

```bash
# Check connectivity
curl -I https://api.midocu.ai/health

# Reinstall with valid license
midocu uninstall
midocu install
```

### Admin creation issues

```bash
# Verify database connection
midocu list-admins --from-container

# Check if company exists
docker exec midocu-backend python -c "from app.core.database import get_db; ..."
```

## Updates

To update to the latest version:

```bash
# Update CLI binary
sudo curl -L -o /usr/local/bin/midocu https://github.com/oxsbilisim/midocu-cli-releases/releases/latest/download/midocu-linux
sudo chmod +x /usr/local/bin/midocu

# Update Docker services
midocu update
```

## Support

- **Email:** support@midocu.ai
- **Documentation:** https://docs.midocu.ai
- **Issues:** https://github.com/oxsbilisim/midocu-cli-releases/issues

---

**Version:** 1.0.18
**Released:** 2026-01-22
