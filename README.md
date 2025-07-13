# Umami Monitoring

This repository manages the self-hosted deployment of the [Umami](https://umami.is) web analytics platform on a private server (e.g. thin client). It uses `docker-compose` for local deployment and will later transition to a Kubernetes-based deployment with GitOps via FluxCD.

## 🔧 Technologies Used

- [Umami](https://umami.is) – open-source web analytics
- [Docker Compose](https://docs.docker.com/compose/)
- [Ansible](https://www.ansible.com/) – infrastructure automation
- [Cloudflared](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/) – private tunnel to Cloudflare
- [GitHub Actions](https://github.com/features/actions) – CI/CD
- [K3s](https://k3s.io/) – lightweight Kubernetes (planned)
- [FluxCD](https://fluxcd.io/) – GitOps automation (planned)

## 📁 Project Structure

```bash
umami-monitoring/
├── docker/
│   └── docker-compose.yml        # Umami stack definition
├── playbooks/
│   └── configure-cloudflared.yml # Ansible playbook for tunnel setup
├── ansible.cfg
├── inventory/
│   ├── hosts.ini                 # Ansible inventory
│   └── host_vars/
│       └── node1hp.yml          # Host-specific variables
├── README.md
```
