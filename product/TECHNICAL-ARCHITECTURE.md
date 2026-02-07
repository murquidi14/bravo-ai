# Technical Architecture — Bravo AI SaaS Platform

*How to deploy AI Command Centers to multiple steel fabricators*

---

## Overview

```
┌──────────────────────────────────────────────────────────────────────────┐
│                         BRAVO AI CLOUD                                    │
│                     (Your Infrastructure)                                 │
│                                                                          │
│  ┌────────────────────────────────────────────────────────────────────┐  │
│  │                        CORE PLATFORM                               │  │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐             │  │
│  │  │   Prompts    │  │  Workflows   │  │ Integrations │             │  │
│  │  │   Library    │  │   Engine     │  │   Layer      │             │  │
│  │  └──────────────┘  └──────────────┘  └──────────────┘             │  │
│  │                     🔒 PROTECTED IP                                │  │
│  └────────────────────────────────────────────────────────────────────┘  │
│                                 │                                        │
│         ┌───────────────────────┼───────────────────────┐               │
│         │                       │                       │               │
│         ▼                       ▼                       ▼               │
│  ┌─────────────┐        ┌─────────────┐        ┌─────────────┐         │
│  │  CLIENT A   │        │  CLIENT B   │        │  CLIENT C   │         │
│  │ ABC Steel   │        │ XYZ Fab     │        │ 123 Iron    │         │
│  │             │        │             │        │             │         │
│  │ Config:     │        │ Config:     │        │ Config:     │         │
│  │ -PowerFab   │        │ -FabSuite   │        │ -PowerFab   │         │
│  │ -3 users    │        │ -8 users    │        │ -12 users   │         │
│  │ -Pro tier   │        │ -Starter    │        │ -Enterprise │         │
│  └─────────────┘        └─────────────┘        └─────────────┘         │
│         │                       │                       │               │
└─────────│───────────────────────│───────────────────────│───────────────┘
          │                       │                       │
          ▼                       ▼                       ▼
   ┌─────────────┐        ┌─────────────┐        ┌─────────────┐
   │ @ABCSteelBot│        │ @XYZFabBot  │        │ @123IronBot │
   │  Telegram   │        │  Telegram   │        │  Telegram   │
   └─────────────┘        └─────────────┘        └─────────────┘
          │                       │                       │
          ▼                       ▼                       ▼
   ┌─────────────┐        ┌─────────────┐        ┌─────────────┐
   │ 👷 ABC Team │        │ 👷 XYZ Team │        │ 👷 123 Team │
   │   Phones    │        │   Phones    │        │   Phones    │
   └─────────────┘        └─────────────┘        └─────────────┘
```

---

## Current Setup (Del Bravo = Your Prototype)

What you have now:

```
Mac Mini (rentamac)
├── OpenClaw Gateway
│   └── workspace-business/     ← Don Fierro config
│       ├── AGENTS.md
│       ├── SOUL.md
│       ├── integrations/
│       │   ├── powerfab/
│       │   └── email/
│       └── memory/
│           ├── estimating-parameters.md
│           ├── po-workflow.md
│           └── ...
```

**This IS your prototype.** The technical pattern is already proven.

---

## Multi-Client Architecture

### Option 1: Separate Workspaces (Recommended to Start)

Each client gets their own OpenClaw workspace on your server:

```
/var/bravo-ai/
├── core/                          ← 🔒 Your protected IP
│   ├── prompts/
│   │   ├── shop-ops.md
│   │   ├── purchasing.md
│   │   ├── shipping.md
│   │   └── ...
│   ├── workflows/
│   │   ├── bid-tracking.md
│   │   ├── po-workflow.md
│   │   └── ...
│   └── integrations/
│       ├── powerfab/
│       ├── fabsuite/
│       └── procore/
│
├── clients/                       ← Client-specific configs
│   ├── abc-steel/
│   │   ├── config.yaml           ← Their API keys, users, settings
│   │   ├── workspace/            ← Their OpenClaw workspace
│   │   │   ├── AGENTS.md         ← Points to core prompts
│   │   │   ├── SOUL.md           ← Customized for them
│   │   │   └── memory/           ← Their conversation history
│   │   └── .env                  ← Their secrets (encrypted)
│   │
│   ├── xyz-fab/
│   │   ├── config.yaml
│   │   ├── workspace/
│   │   └── .env
│   │
│   └── 123-iron/
│       ├── config.yaml
│       ├── workspace/
│       └── .env
│
└── platform/                      ← Management tools
    ├── deploy-client.sh          ← Script to onboard new client
    ├── billing/                  ← Usage tracking, invoicing
    └── monitoring/               ← Health checks, alerts
```

### How Core Prompts Stay Protected

Client's AGENTS.md doesn't contain the prompts — it REFERENCES them:

```markdown
# AGENTS.md - ABC Steel

## System
You are an AI operations assistant for ABC Steel.
Follow all instructions in the core system.

## Core Behaviors
@import /var/bravo-ai/core/prompts/shop-ops.md
@import /var/bravo-ai/core/prompts/purchasing.md

## Client-Specific Rules
- Shop hours: 6am-4:30pm
- Primary contact: John Smith
- PowerFab instance: abc-steel.powerfab.com
```

The client workspace USES the core prompts but never contains them.

---

## Server Requirements

### Starter (1-5 Clients)
- **Your Mac Mini** — Already have this!
- Or: DigitalOcean Droplet $20-40/mo
- Or: AWS Lightsail $20-40/mo

### Growth (5-20 Clients)  
- VPS: 4 CPU, 8GB RAM, 100GB SSD
- ~$50-100/month
- DigitalOcean, Linode, or Vultr

### Scale (20+ Clients)
- Dedicated server or cloud instances
- Container orchestration (Docker Swarm or Kubernetes)
- ~$200-500/month
- Consider managed services

---

## Client Onboarding Process

### Step 1: Create Telegram Bot
```bash
# In BotFather:
/newbot
Name: ABC Steel Assistant
Username: ABCSteelBot

# Save the token
```

### Step 2: Run Deploy Script
```bash
./deploy-client.sh \
  --name "abc-steel" \
  --company "ABC Steel Fabricators" \
  --telegram-token "BOT_TOKEN_HERE" \
  --tier "professional" \
  --powerfab-url "https://abc.powerfab.com" \
  --powerfab-key "API_KEY_HERE" \
  --admin-phone "+19155551234"
```

### Step 3: Script Does Everything
```bash
#!/bin/bash
# deploy-client.sh

CLIENT_NAME=$1
# ... parse args ...

# Create directory structure
mkdir -p /var/bravo-ai/clients/$CLIENT_NAME/{workspace,logs}

# Generate config
cat > /var/bravo-ai/clients/$CLIENT_NAME/config.yaml << EOF
client:
  name: $COMPANY
  slug: $CLIENT_NAME
  tier: $TIER
  created: $(date -I)

telegram:
  bot_token: $TELEGRAM_TOKEN
  
integrations:
  powerfab:
    url: $POWERFAB_URL
    api_key: $POWERFAB_KEY

users:
  admin:
    phone: $ADMIN_PHONE
    role: admin
EOF

# Copy workspace template
cp -r /var/bravo-ai/core/templates/workspace/* \
      /var/bravo-ai/clients/$CLIENT_NAME/workspace/

# Generate OpenClaw config
cat > /var/bravo-ai/clients/$CLIENT_NAME/openclaw.yaml << EOF
# OpenClaw config for $CLIENT_NAME
model: anthropic/claude-sonnet-4-20250514
workspace: /var/bravo-ai/clients/$CLIENT_NAME/workspace

channels:
  telegram:
    token: $TELEGRAM_TOKEN
    allowlist:
      - $ADMIN_PHONE
EOF

# Start the gateway
openclaw gateway start --config /var/bravo-ai/clients/$CLIENT_NAME/openclaw.yaml

echo "✅ $CLIENT_NAME deployed!"
echo "Bot: @${CLIENT_NAME}Bot"
```

### Step 4: Initial Configuration
- Add authorized users
- Connect to their PowerFab/FabSuite
- Customize SOUL.md for their company
- Run test conversations

---

## Process Management

### Running Multiple Gateways

Each client runs their own OpenClaw gateway process:

```bash
# Using PM2 (Node.js process manager)
pm2 start openclaw --name "abc-steel" -- gateway start \
  --config /var/bravo-ai/clients/abc-steel/openclaw.yaml

pm2 start openclaw --name "xyz-fab" -- gateway start \
  --config /var/bravo-ai/clients/xyz-fab/openclaw.yaml

pm2 start openclaw --name "123-iron" -- gateway start \
  --config /var/bravo-ai/clients/123-iron/openclaw.yaml

# View all
pm2 list

# Monitor
pm2 monit
```

### Alternative: Docker Containers

```yaml
# docker-compose.yaml
version: '3.8'

services:
  abc-steel:
    image: openclaw:latest
    volumes:
      - ./core:/app/core:ro          # Read-only core
      - ./clients/abc-steel:/app/client
    environment:
      - CONFIG_PATH=/app/client/openclaw.yaml
    restart: unless-stopped

  xyz-fab:
    image: openclaw:latest
    volumes:
      - ./core:/app/core:ro
      - ./clients/xyz-fab:/app/client
    environment:
      - CONFIG_PATH=/app/client/openclaw.yaml
    restart: unless-stopped
```

---

## Access Control & Billing

### User Management Per Client

```yaml
# clients/abc-steel/config.yaml
users:
  - phone: "+19155551234"
    name: "John Smith"
    role: admin
    
  - phone: "+19155555678"
    name: "Mike Johnson"  
    role: user
    features:
      - shop_status
      - shipping
      
  - phone: "+19155559999"
    name: "Sarah Davis"
    role: user
    features:
      - purchasing
      - inventory
```

### Usage Tracking

```python
# billing/usage_tracker.py

def log_usage(client_id, event_type, tokens_used):
    """Track usage for billing"""
    db.insert({
        'client': client_id,
        'timestamp': datetime.now(),
        'event': event_type,  # 'message', 'api_call', etc.
        'tokens': tokens_used,
        'cost': calculate_cost(tokens_used)
    })

def monthly_report(client_id):
    """Generate monthly usage report"""
    usage = db.query(client_id, this_month)
    return {
        'messages': usage.count(),
        'tokens': usage.sum('tokens'),
        'api_calls': usage.count('api_call'),
        'estimated_cost': usage.sum('cost')
    }
```

### Tier Enforcement

```yaml
# Tier limits
tiers:
  starter:
    max_users: 5
    max_messages_per_day: 100
    features:
      - shop_status
      - alerts
      - email
    integrations:
      - telegram
      
  professional:
    max_users: 20
    max_messages_per_day: 500
    features:
      - shop_status
      - alerts
      - email
      - purchasing
      - shipping
      - inventory
    integrations:
      - telegram
      - sms
      - powerfab
      
  enterprise:
    max_users: unlimited
    max_messages_per_day: unlimited
    features: all
    integrations: all
```

---

## Security Checklist

### Server Security
- [ ] SSH key authentication only (no passwords)
- [ ] Firewall (only ports 22, 443)
- [ ] Automatic security updates
- [ ] Encrypted backups

### Client Data Isolation
- [ ] Each client in separate directory
- [ ] No cross-client data access
- [ ] Secrets in encrypted .env files
- [ ] API keys never in code

### Core IP Protection
- [ ] Core directory read-only to client processes
- [ ] No direct file access for clients
- [ ] Prompts loaded at runtime, never copied
- [ ] Git repo private, limited access

---

## Monitoring & Alerts

```bash
# Health check script
#!/bin/bash

for client in /var/bravo-ai/clients/*/; do
    name=$(basename $client)
    
    # Check if process running
    if ! pm2 show $name > /dev/null 2>&1; then
        alert "⚠️ $name gateway is DOWN"
    fi
    
    # Check last activity
    last_msg=$(stat -c %Y $client/workspace/memory/*.md | sort -rn | head -1)
    if [ $(($(date +%s) - last_msg)) -gt 86400 ]; then
        alert "⚠️ $name no activity in 24h"
    fi
done
```

---

## Quick Start: Your First External Client

### Week 1: Prep
1. Set up cloud server (DigitalOcean $20/mo)
2. Install OpenClaw
3. Create directory structure
4. Write deploy script

### Week 2: Pilot Client
1. Sign up pilot client (maybe free/discounted)
2. Create their Telegram bot
3. Deploy their instance
4. Configure integrations
5. Train their team

### Week 3: Iterate
1. Gather feedback
2. Fix issues
3. Improve onboarding process
4. Document everything

### Week 4: Launch
1. Open for business
2. First paying client
3. Refine, repeat

---

## Cost Structure

### Your Costs Per Client

| Item | Monthly Cost |
|------|--------------|
| Server (amortized) | $5-10 |
| AI API (Claude/OpenAI) | $20-100* |
| Telegram | FREE |
| Your time (support) | Variable |

*AI costs depend on usage — pass through to client or include in pricing.

### Pricing vs. Costs

| Tier | You Charge | Your Cost | Gross Margin |
|------|------------|-----------|--------------|
| Starter $500 | $500 | ~$50 | ~$450 (90%) |
| Professional $1,500 | $1,500 | ~$100 | ~$1,400 (93%) |
| Enterprise $3,500 | $3,500 | ~$200 | ~$3,300 (94%) |

SaaS margins are beautiful. 📈

---

## Next Steps

1. **Set up cloud server** — DigitalOcean or similar
2. **Create deploy script** — Automate client onboarding
3. **Build admin dashboard** — (later) web UI to manage clients
4. **Document onboarding** — Step-by-step for each new client
5. **First pilot client** — Real-world validation

---

*This is your playbook. Del Bravo is the proof it works. Now scale it.*
