# Pelican Panel - Coolify Deployment

This repository contains a Docker Compose setup for deploying Pelican Panel using Coolify.

## Features

- **Pelican Panel**: Web-based game server management panel
- **Pelican Wings**: Daemon for managing game servers
- **SQLite Database**: Lightweight database (can be changed to MySQL/MariaDB)
- **Built-in Web Server**: Panel includes its own web server
- **Persistent Storage**: All data persists across deployments
- **Coolify Integration**: Optimized for deployment with Coolify

## Quick Start with Coolify

### 1. Prerequisites

- A Coolify instance running
- A server resource configured in Coolify
- Domain name pointing to your server (for SSL)

### 2. Deploy to Coolify

1. **Create a new project** in Coolify
2. **Add a Git source** pointing to this repository (or upload files manually)
3. **Add a service** with these settings:
   - **Docker Compose File**: `docker-compose.yml`
   - **Environment Variables**: Copy from `.env.example` and customize

### 3. Configure Environment Variables

Copy `.env.example` to `.env` and update these values:
   - `APP_URL`: Your actual domain (e.g., `https://panel.yourdomain.com`)
   - `APP_TIMEZONE`: Your timezone (e.g., `America/New_York`)
   - Keep other settings as default (SQLite database is recommended for getting started)

### 4. Deploy

Click "Deploy" in Coolify. The deployment will:
- Set up persistent volumes for data storage
- Configure networking between services

### 5. Initial Setup

1. Wait for deployment to complete (check logs)
2. Visit `https://your-domain.com/installer` to complete setup
3. Follow the installation wizard:
   - Enter your email and create admin account
   - Choose database (SQLite is recommended for getting started)
   - Complete the setup process

### 6. Configure Wings (Optional)

If you want to run game servers on this machine:

1. In the Panel, go to Admin → Nodes → New Node
2. Set the connection details to `localhost` or your server IP
3. Copy the generated token to your `.env` file as `WINGS_TOKEN`
4. Redeploy the service

## Ports Used

- **80**: Panel web interface (internal - Coolify handles external access)
- **8443**: Wings daemon (internal)
- **2022**: Wings API (internal)

Coolify will handle external access through its reverse proxy.

## Database Options

### SQLite (Default)
- Lightweight and easy to set up
- Good for small deployments
- Data stored in Docker volume

### MySQL/MariaDB (Advanced)
For larger deployments, you can switch to MySQL:

1. Add a MySQL service in Coolify
2. Update environment variables:
   ```bash
   DB_CONNECTION=mysql
   DB_HOST=mysql-service-name
   DB_DATABASE=pelican
   DB_USERNAME=pelican
   DB_PASSWORD=your_password
   ```

## Troubleshooting

### Common Issues

1. **SSL Certificate Issues**: Ensure your domain points to the correct IP
2. **Port Conflicts**: Make sure ports 8080, 8443, 2022 aren't used by other services
3. **Permission Issues**: Wings needs Docker socket access (configured in compose file)

### Logs

Check service logs in Coolify for detailed error information.

## Security Notes

- Change default passwords after installation
- Use strong, unique passwords
- Keep your server and Docker images updated
- Consider using a firewall to restrict access

## Support

- [Pelican Panel Documentation](https://pelican.dev/docs/)
- [Coolify Documentation](https://coolify.io/docs/)
- [Pelican Discord](https://discord.gg/pelican) for community support
