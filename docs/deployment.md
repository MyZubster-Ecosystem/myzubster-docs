# MyZubster Deployment Guide

## Production Deployment

### Option 1: Docker Compose (Recommended)

1. Clone the repository on your server:
```bash
git clone https://github.com/MyZubster-Ecosystem/MyZubsterGateway.git
cd MyZubsterGateway
```

2. Configure environment:
```bash
cp .env.example .env.production
# Edit with production values
```

3. Build and start:
```bash
docker compose -f docker-compose.prod.yml up -d --build
```

4. Verify:
```bash
docker compose ps
curl http://localhost:3000/api/health
```

### Option 2: Manual Deployment

#### Prerequisites
- Ubuntu 22.04 LTS
- Node.js 18 LTS
- PostgreSQL 16
- Redis 7
- Nginx (reverse proxy)
- PM2 (process manager)

#### Steps

1. Install Node.js:
```bash
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs
```

2. Install PM2:
```bash
npm install -g pm2
```

3. Clone and build:
```bash
git clone https://github.com/MyZubster-Ecosystem/MyZubsterGateway.git
cd MyZubsterGateway
npm ci
npm run build
```

4. Start with PM2:
```bash
pm2 start npm --name "myzubster" -- start
pm2 save
pm2 startup
```

5. Configure Nginx:
```nginx
server {
    listen 80;
    server_name myzubster.com;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

6. Enable SSL with Certbot:
```bash
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d myzubster.com
```

### Option 3: Vercel (Gateway Only)

The Next.js gateway can be deployed to Vercel:

```bash
npm i -g vercel
vercel --prod
```

Note: Backend services (bounty, marketplace, wallet) must still be deployed separately.

## Monitoring

### Health Check Endpoint
```
GET /api/health
```
Returns:
```json
{
  "status": "ok",
  "services": {
    "database": "connected",
    "redis": "connected",
    "bounty_service": "healthy",
    "marketplace": "healthy",
    "wallet": "healthy"
  },
  "uptime": 86400
}
```

### Logs
```bash
# PM2 logs
pm2 logs myzubster

# Docker logs
docker compose logs -f gateway

# System logs
journalctl -u nginx -f
```

## Backup

### Database
```bash
pg_dump -U myzubster myzubster > backup_$(date +%Y%m%d).sql
```

### Automated (cron)
```cron
0 2 * * * pg_dump -U myzubster myzubster | gzip > /backups/myzubster_$(date +\%Y\%m\%d).sql.gz
0 3 * * * find /backups -name '*.gz' -mtime +7 -delete
```

## Rollback

```bash
# Docker
docker compose down
docker compose -f docker-compose.prod.yml up -d --build

# PM2
pm2 stop myzubster
git checkout <previous-commit>
npm ci && npm run build
pm2 start myzubster
```
