# DEPLOY.md — [Project Name]
> Deployment configuration, steps, and history.
> Agent: update the deploy log section after every deployment.

---

## Environments

### Staging
- **Host:** [VPS provider and plan]
- **IP:** [staging server IP]
- **URL:** [staging URL]
- **Branch:** `main`
- **Deploy:** manual via `./kit deploy`

### Production
- **Host:** [VPS provider and plan]
- **IP:** [production server IP]
- **URL:** [production URL]
- **Branch:** `main`
- **Deploy:** manual via `./kit deploy --prod`

---

## Server Setup (one-time, done manually)

### 1. Access Server
```bash
ssh root@[server-ip]
```

### 2. Create Deploy User
```bash
adduser deploy
usermod -aG sudo deploy
# Copy your SSH public key to deploy user's authorized_keys
```

### 3. Install Runtime
```bash
# Node.js (adjust version as needed)
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs
```

### 4. Install PM2
```bash
npm install -g pm2
```

### 5. Install Nginx
```bash
sudo apt install nginx
sudo systemctl enable nginx
```

### 6. Clone Repository
```bash
git clone https://github.com/[username]/[repo].git /var/www/[project]
```

### 7. Set Environment Variables
```bash
cp /var/www/[project]/.env.example /var/www/[project]/.env
nano /var/www/[project]/.env
# Fill in all values — refer to ENV.md for the full list
```

### 8. Nginx Configuration
```nginx
server {
    listen 80;
    server_name [your-domain.com];

    location / {
        proxy_pass http://localhost:[PORT];
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

### 9. SSL Certificate
```bash
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d [your-domain.com]
# Auto-renewal verification:
sudo certbot renew --dry-run
```

### 10. Start with PM2
```bash
cd /var/www/[project]
pm2 start [start-command] --name [project-name]
pm2 save
pm2 startup
```

---

## Standard Deploy Process

```bash
# On server
ssh deploy@[server-ip]
cd /var/www/[project]
git pull origin main
npm install --production
npm run build              # if build step needed
npx prisma migrate deploy  # if DB migrations needed
pm2 restart [project-name]

# Verify
curl https://[your-domain.com]/health
```

---

## Rollback Procedure

```bash
# Find previous commit
git log --oneline -10

# Roll back
git checkout [previous-commit-hash]
pm2 restart [project-name]

# Or revert and redeploy
git revert HEAD
git push origin main
# Then run standard deploy
```

---

## Health Check

App exposes `/health` endpoint returning:
```json
{ "status": "ok", "timestamp": "2025-03-16T10:00:00Z" }
```

---

## Deploy History

| Date | Target | Commit | Status | Notes |
|---|---|---|---|---|
| — | — | — | — | — |
