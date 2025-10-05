# Portfolio Site

Personal portfolio website deployed with Ansible automation.

## Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/codelikesuraj/portfolio-site.git
   cd portfolio-site
   ```

2. **Configure variables**
   ```bash
   cp vars.yml.example vars.yml
   ```

   Edit `vars.yml` with your actual values:
   - `domain_name`: Your domain
   - `email`: Your email for Let's Encrypt
   - `server_ip`: Your server IP address
   - `ansible_user`: SSH username
   - `ansible_ssh_private_key_file`: Path to your SSH key

## Deployment

**Test connection first:**

```bash
ansible -i inventory.yml webservers -m ping -e @vars.yml
```

**Run the playbook to deploy:**

```bash
ansible-playbook -i inventory.yml site.yml -K
```

The `-K` flag prompts for the sudo password (required for non-root users).

This will:
- Install NGINX and Certbot
- Deploy web content to `/var/www/html`
- Configure SSL certificates with Let's Encrypt
- Set up automatic HTTPS redirects

## Project Structure

```
.
├── site.yml            # Ansible playbook
├── inventory.yml       # Server inventory (uses vars.yml)
├── vars.yml            # Configuration variables (gitignored)
├── vars.yml.example    # Template for configuration
├── web-content/        # Static website files
└── README.md
```

## Requirements

- Ansible installed locally
- Ubuntu server with sudo access
- SSH key configured for server access
- Domain DNS pointing to server IP