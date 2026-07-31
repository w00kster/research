# Free Claude Code (FCC) Setup Guide

This document provides a template and guidelines for setting up Free Claude Code (FCC) in a secure, reproducible manner. It shows the structure and configuration needed without exposing any sensitive credentials.

## 📋 Overview

This setup runs Free Claude Code (fcc-server) as a systemd service with:
- Telegram bot support (configurable for single or multi-user)
- UV-based Python environment isolation
- Persistent storage and logging
- Integration with a research repository for knowledge management

## 📁 Directory Structure

```
/opt/fcc/
├── .fcc/                   # Configuration directory
│   ├── .env                # Environment variables (API keys, Telegram config) - **KEEP SECRET**
│   ├── .env.example        # Template/example version (safe to share)
│   ├── agent_workspace/    # Agent workspace directory
│   ├── codex-model-catalog.json
│   └── logs/               # Application logs
├── bots/                   # Bot instances
│   ├── open-connector/     # (Optional - separate bot implementation)
│   └── research/           # GitHub-connected research repository
├── .local/                 # UV Python environment
│   └── share/uv/tools/free-claude-code/  # FCC installation
├── fcc-server-wrapper.sh   # Wrapper script to source env and start server
├── .gitconfig              # Git configuration (safe directory for research repo)
└── .claude/                # Claude Code configuration
```

## 🔧 Installation & Setup

### Prerequisites
- Ubuntu/Debian-based system
- Root/sudo access
- Internet access for package installation
- GitHub account (for research repository)
- Telegram Bot Token (from @BotFather)
- API keys for desired AI providers (NVIDIA NIM, OpenRouter, etc.)

### FCC Installation
1. Install UV package manager:
   ```bash
   curl -LsSf https://astral.sh/uv/install.sh | sh
   ```

2. Install FCC via UV (official method):
   ```bash
   uv pip install --git https://github.com/free-claude-code/free-claude-code
   ```
   This installs to `~/.local/share/uv/tools/free-claude-code/` by default

3. Create system user for service:
   ```bash
   sudo useradd -r -s /usr/bin/nologin fcc
   sudo mkdir -p /opt/fcc
   sudo chown fcc:fcc /opt/fcc
   ```

4. Copy FCC installation to `/opt/fcc/.local/share/uv/tools/free-claude-code/` (or adjust paths accordingly)

### Configuration

#### Environment Template (`/opt/fcc/.fcc/.env.example`)
Create this as a template - **never commit actual .env files**:
```ini
# ===== TELEGRAM CONFIGURATION =====
MESSAGING_PLATFORM="telegram"
TELEGRAM_BOT_TOKEN="your_telegram_bot_token_here"  # Get from @BotFather
# For single user: ALLOWED_TELEGRAM_USER_ID=123456789
# For multiple users: ALLOWED_TELEGRAM_USER_ID=111111111,222222222,333333333
ALLOWED_TELEGRAM_USER_ID=your_user_id_here,another_user_id_here
MESSAGING_RATE_LIMIT=1
MESSAGING_RATE_WINDOW=1

# ===== AI PROVIDER CONFIGURATION =====
# Select ONE primary provider for the MODEL setting below
# Format: provider_type/model/name
# Valid providers: "nvidia_nim" | "open_router" | "gemini" | "deepseek" | "mistral" | 
#                  "mistral_codestral" | "opencode" | "opencode_go" | "vercel" | 
#                  "huggingface" | "cohere" | "github_models" | "wafer" | "kimi" | 
#                  "minimax" | "cerebras" | "groq" | "sambanova" | "fireworks" | 
#                  "cloudflare" | "zai" | "lmstudio" | "llamacpp" | "ollama"

MODEL="nvidia_nim/nvidia/nemotron-3-super-120b-a12b"

# Set API keys for providers you plan to use (leave empty if not used)
NVIDIA_NIM_API_KEY="your_nvidia_nim_key_here"
OPENROUTER_API_KEY="your_openrouter_key_here"
GEMINI_API_KEY="your_gemini_key_here"
DEEPSEEK_API_KEY="your_deepseek_key_here"
MISTRAL_API_KEY="your_mistral_key_here"
CODESTRAL_API_KEY="your_codestral_key_here"
# ... add others as needed

# ===== LOCAL PROVIDERS (NO API KEY NEEDED) =====
LM_STUDIO_BASE_URL="http://localhost:1234/v1"
LLAMACPP_BASE_URL="http://localhost:8080/v1"
OLLAMA_BASE_URL="http://localhost:11434"

# ===== OPTIONAL SETTINGS =====
# Model-specific thinking controls (blank inherits ENABLE_MODEL_THINKING)
ENABLE_OPUS_THINKING=
ENABLE_SONNET_THINKING=
ENABLE_HAIKU_THINKING=
ENABLE_MODEL_THINKING=true

# Provider rate limiting (requests per window)
PROVIDER_RATE_LIMIT=1
PROVIDER_RATE_WINDOW=3
PROVIDER_MAX_CONCURRENCY=5

# HTTP client timeouts (seconds)
HTTP_READ_TIMEOUT=300
HTTP_WRITE_TIMEOUT=60
HTTP_CONNECT_TIMEOUT=60

# Optional server API key (Anthropic-style)
ANTHROPIC_AUTH_TOKEN="freecc"  # Change this in production if desired

# Open /admin in the default browser when fcc-server becomes healthy (set 0/false/no to disable)
FCC_OPEN_BROWSER=true

# Agent file access restriction
ALLOWED_DIR="/opt/fcc/bots/"

# Advanced features (usually safe to leave as shown)
ENABLE_NETWORK_PROBE_MOCK=true
ENABLE_TITLE_GENERATION_SKIP=true
ENABLE_SUGGESTION_MODE_SKIP=true
ENABLE_FILEPATH_EXTRACTION_MOCK=true
ENABLE_WEB_SERVER_TOOLS=true
WEB_FETCH_ALLOWED_SCHEMES=http,https
WEB_FETCH_ALLOW_PRIVATE_NETWORKS=false
```

#### Actual Environment File (`/opt/fcc/.fcc/.env`)
- **COPY** `.env.example` to `.env` and fill in your actual values
- **NEVER** commit `.env` to version control
- Set restrictive permissions: `chmod 600 /opt/fcc/.fcc/.env`
- Ensure only the `fcc` user can read it

#### Systemd Service (`/etc/systemd/system/fcc-server.service`)
```ini
[Unit]
Description=Free Claude Code Server
After=network.target

[Service]
Type=simple
User=fcc
WorkingDirectory=/opt/fcc
EnvironmentFile=/opt/fcc/.fcc/.env
ExecStart=/opt/fcc/.local/share/uv/tools/free-claude-code/bin/fcc-server
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
```

#### Wrapper Script (`/opt/fcc/fcc-server-wrapper.sh`)
```bash
#!/bin/bash
set -a
source /opt/fcc/.fcc/.env
set +a
exec /opt/fcc/.local/share/uv/tools/free-claude-code/bin/fcc-server
```

#### Research Repository Setup
1. Clone repository as user `fcc`:
   ```bash
   sudo -u fcc git clone https://github.com/yourusername/your-research-repo.git /opt/fcc/bots/research
   ```

2. Configure git safety (run once):
   ```bash
   git config --global --add safe.directory /opt/fcc/bots/research
   ```
   (This creates/updates `~/.gitconfig` or `/opt/fcc/.gitconfig`)

## 🔐 Security Best Practices

### Environment Variables
1. **Never** commit `.env` files to git
2. Add to `.gitignore`:
   ```
   # Environment files
   .fcc/.env
   .fcc/.env.*
   !.fcc/.env.example  # Keep the template
   ```
3. Use `.env.example` as a template for new setups
4. Consider using a secrets manager for production deployments

### File Permissions
```bash
# Set ownership to fcc user
sudo chown -R fcc:fcc /opt/fcc/

# Set restrictive permissions on env file
sudo chmod 600 /opt/fcc/.fcc/.env

# Ensure logs directory is accessible
sudo chmod 750 /opt/fcc/.fcc/logs
sudo chown fcc:fcc /opt/fcc/.fcc/logs
```

### Network Security
- The FCC server binds to localhost by default - external access requires:
  - A reverse proxy (nginx, Caddy, Traefik)
  - Proper authentication if exposing externally
  - Consider limiting to localhost-only for maximum security

### Telegram Bot Security
- The `ALLOWED_TELEGRAM_USER_ID` setting restricts bot access to specific Telegram user IDs
- To find your Telegram user ID, interact with @userinfobot or @getmyid_bot
- Only add trusted user IDs to the comma-separated list
- Unauthorized users will see their messages ignored (logged as warnings)

## 🚀 Service Management

### Start/Stop/Restart
```bash
sudo systemctl start fcc-server
sudo systemctl stop fcc-server
sudo systemctl restart fcc-server
sudo systemctl status fcc-server
```

### Enable on Boot
```bash
sudo systemctl enable fcc-server
```

### View Logs
```bash
sudo journalctl -u fcc-server -f
```
Logs also appear in `/opt/fcc/.fcc/logs/`

## 🔄 Backup & Recovery

### Critical Files to Backup (EXCLUDING SECRETS)
1. `/opt/fcc/fcc-server-wrapper.sh` - Wrapper script
2. `/etc/systemd/system/fcc-server.service` - Service definition
3. `/opt/fcc/.fcc/.env.example` - Environment template (NOT .env)
4. `/opt/fcc/bots/research/` - Your research repository (GitHub-backed)
5. `/opt/fcc/.gitconfig` - Git safety configuration
6. This setup guide and any custom documentation

### Backup Procedure (Safe for Sharing)
```bash
# Create timestamped backup directory
mkdir -p /root/fcc-backup-$(date +%Y%m%d)

# Copy NON-SENSITIVE files
sudo cp /opt/fcc/fcc-server-wrapper.sh /root/fcc-backup-$(date +%Y%m%d)/
sudo cp /etc/systemd/system/fcc-server.service /root/fcc-backup-$(date +%Y%m%d)/
sudo cp /opt/fcc/.fcc/.env.example /root/fcc-backup-$(date +%Y%m%d)/
sudo cp -r /opt/fcc/.fcc/logs/ /root/fcc-backup-$(date +%Y%m%d)/logs/  # Optional - may contain sensitive data!
sudo cp /opt/fcc/.gitconfig /root/fcc-backup-$(date +%Y%m%d)/

# Research repo is already on GitHub, but local backup also possible (review first!):
# sudo -u fcc cp -r /opt/fcc/bots/research/ /root/fcc-backup-$(date +%Y%m%d)/research-review/
```

> ⚠️ **Warning**: Logs may contain sensitive information! Review log contents before backing up or sharing.

### Restore Procedure
1. Reinstall FCC following installation steps above
2. Stop service: `sudo systemctl stop fcc-server`
3. Restore NON-SENSITIVE configuration files to their original locations
4. Create `.env` from `.env.example` and add your actual secrets
5. Set correct ownership: `sudo chown -R fcc:fcc /opt/fcc/`
6. Set correct permissions: `sudo chmod 600 /opt/fcc/.fcc/.env`
7. Reload systemd: `sudo systemctl daemon-reload`
8. Start service: `sudo systemctl start fcc-server`

## 🔄 Making This Reproducible (IaC/CaC Ready)

For future conversion to Infrastructure as Code (Ansible, NixOS, etc.), these components should be automated:

### Ansible Playbook Structure (Conceptual)
```yaml
- hosts: fcc_servers
  vars:
    fcc_user: fcc
    fcc_install_dir: /opt/fcc
    # SECRETS SHOULD COME FROM VAULT OR ENCRYPTED VARIABLES
    telegram_bot_token: "{{ vault_telegram_bot_token }}"
    telegram_user_ids: ["111111111", "222222222"]  # Example IDs
    nvidia_nim_api_key: "{{ vault_nvidia_nim_key }}"
    # ... other secrets from vault
  tasks:
    # ... tasks to install UV, create user, deploy templates, etc.
    # Deploy environment TEMPLATE only
    - name: Deploy environment template
      copy:
        src: fcc.env.example
        dest: "{{ fcc_install_dir }}/.fcc/.env.example"
        owner: "{{ fcc_user }}"
        group: "{{ fcc_user }}"
        mode: '0644'
    # Note: Actual .env should be deployed separately via secure secrets management
```

### Key Parameters for Automation (Use Secrets Management!)
When creating IaC templates, these variables NEED to be protected:
- `TELEGRAM_BOT_TOKEN` (MUST BE ENCRYPTED/SECRET)
- `NVIDIA_NIM_API_KEY` (MUST BE ENCRYPTED/SECRET)
- `OPENROUTER_API_KEY` (MUST BE ENCRYPTED/SECRET)
- `ALLOWED_TELEGRAM_USER_ID` (Consider if this needs protection - user IDs are less sensitive but still reveal who can access the bot)
- `MODEL` (Generally safe - indicates provider/model choice)
- Repository URL for research bot
- File paths and user/group names

## 📱 Telegram Multi-User Details

The Telegram implementation supports multiple users through comma-separated IDs in `ALLOWED_TELEGRAM_USER_ID`:

### Example Configuration
```
ALLOWED_TELEGRAM_USER_ID=111111111,222222222,333333333
```

### How It Works
1. The FCC Telegram parser splits the value by commas
2. Each incoming message's `user.id` is checked against this list
3. If the user ID is not in the allowed list, the message is ignored/logged as unauthorized
4. This applies to both text messages and voice notes

### Finding Your Telegram User ID
- Start a chat with @userinfobot
- Or use @getmyid_bot
- Or check https://t.me/MyTelegramID_bot
- The bot will reply with your numeric user ID

### Adding/Removing Users
1. Update `/opt/fcc/.fcc/.env`: 
   ```ini
   ALLOWED_TELEGRAM_USER_ID=111111111,222222222,444444444
   ```
2. Restart the service:
   ```bash
   sudo systemctl restart fcc-server
   ```

## 📚 Research Repository Workflow

Following the principles in agentic workflow documentation:

### Adding New Research Topics
1. Navigate to appropriate category:
   ```bash
   cd /opt/fcc/bots/research/Topics/
   mkdir -p Software/my-new-topic
   cd Software/my-new-topic
   ```

2. Create markdown file with metadata:
   ```markdown
   # My New Topic
   Added: 2024-01-15
   Status: [Active/Archived/Backlog]
   Tags: [tag1, tag2, tag3]

   ## Summary
   Brief description of the topic...

   ## Key Points
   - Point 1
   - Point 2

   ## Resources
   - [Resource Name](https://example.com) - Description

   ## Related Topics
   - [[Related Topic Name]]
   ```

3. Commit changes:
   ```bash
   git add Software/my-new-topic/topic-name.md
   git commit -m "Add: My New Topic in Software"
   git push origin main
   ```

### Project Tracking
Update `/opt/fcc/bots/research/Projects/README.md` to track active work:
```markdown
### [Project Name]

**Status**: [Active/Planned/Paused]  
**Relevant Topics**: [[Topic 1]], [[Topic 2]]  
**Description**: Brief overview of what this project entails.

**Progress**:
- [ ] Milestone 1
- [ ] Milestone 2
```

## 🛠️ Maintenance

### Regular Tasks
1. **Check Service Status**: `sudo systemctl status fcc-server`
2. **Review Logs**: `sudo journalctl -u fcc-server --since "1 day ago"` (review for sensitive data first!)
3. **Update FCC**: Periodically re-install via UV to get latest features
4. **Backup Template**: After any configuration structure (not the actual .env which contains secrets)
5. **Monitor Disk Space**: Especially in `/opt/fcc/.fcc/logs/`

### Update FCC
```bash
# As user fcc
cd /opt/fcc/.local/share/uv/tools/free-claude-code/
git pull
uv pip install -e .  # Reinstall in development mode
sudo systemctl restart fcc-server
```

## 📝 What's Safe to Share vs. What's Secret

### ✅ SAFE TO SHARE / COMMIT TO GIT
- This setup guide
- Directory structure explanations
- Installation procedures
- Service file structure (without actual values)
- Wrapper script
- Environment TEMPLATE (`.env.example`)
- Research repository structure and guidelines
- Workflow practices and documentation
- Non-secret configuration explanations
- Examples with fake values
- Systemd service file (without EnvironmentFile value if it points to secret)

### 🔐 KEEP SECRET / NEVER COMMIT
- Actual `.env` file containing:
  - API keys (NVIDIA_NIM_API_KEY, TELEGRAM_BOT_TOKEN, etc.)
  - Any other secrets
- Log files (may contain sensitive data from conversations)
- Any files containing actual credentials or tokens

### 🔧 RECOMMENDED GITIGNORE ADDITIONS
```bash
# In your /opt/fcc/.gitconfig or repository .gitignore:
.fcc/.env
.fcc/.env.*
.fcc/logs/*
# Optional: be more specific about log files if they contain PII
# But when in doubt, exclude logs from shared backups unless reviewed
```

## 📄 Verification

To verify your setup matches safe practices:

1. **Check .env is not tracked**:
   ```bash
   cd /opt/fcc
   git status --ignored
   # .env should NOT appear in the output
   ```

2. **Verify .env.example exists**:
   ```bash
   ls -la /opt/fcc/.fcc/.env.example
   # Should exist and contain template values
   ```

3. **Confirm Research Repository**:
   ```bash
   cd /opt/fcc/bots/research
   git remote -v
   # Should show your research repository URL
   git status
   # Should show clean working tree (if no local changes)
   ```

4. **Test .gitprotections**:
   ```bash
   # Try to add .env - should be ignored by gitignore
   touch /opt/fcc/.fcc/.env.test
   git add /opt/fcc/.fcc/.env.test
   git status
   # .env.test should NOT show as staged for commit
   rm /opt/fcc/.fcc/.env.test
   ```

## 🆘 Troubleshooting (Security-Related)

### If You Accidentally Commit Secrets
1. **Immediately revoke/compromise all exposed keys**
2. Remove the commit from history (if recently pushed):
   ```bash
   # WARNING: History rewriting - use with caution
   git filter-branch --force --index-filter \
     'git rm --cached --ignore-unmatch .fcc/.env' \
     --prune-empty --tag-name-filter cat -- --all
   ```
   OR use [BFG Repo-Cleaner](https://rtyley.github.io/bfg-repo-cleaner/)
3. Force push the cleaned history
4. Notify anyone who may have fetched the compromised repository
5. Consider the keys compromised and rotate them

### Logs Containing Sensitive Data
1. Review `/opt/fcc/.fcc/logs/` periodically
2. Consider adjusting log levels if too verbose
3. Never back up or share logs without review
4. In production, consider log redaction or secure log storage

## 📄 License & Acknowledgements

This setup guide is based on:
- [Free Claude Code](https://github.com/free-claude-code/free-claude-code) (MIT License)
- Community best practices for secure API key management
- Standard Linux service security principles

---

**Remember**: The strength of your setup depends on keeping your secrets secret. 
When in doubt, treat any configuration value as potentially sensitive until verified otherwise.

*Document last updated: $(date +%Y-%m-%d)*
*Safe for sharing and committing to public repositories*