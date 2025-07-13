# 📈 Umami Monitoring

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
├── README.md
```

In [ansible-configs](https://github.com/przemyslaw-koz/ansible-configs) repository under [00-ansible-monitoring](https://github.com/przemyslaw-koz/ansible-configs/tree/main/00-umami-monitoring)

```bash
00-ansible-monitoring
├── playbooks/
│   └── configure-cloudflared.yml # Ansible playbook for tunnel setup
├── ansible.cfg
├── inventory/
│   ├── hosts.ini                 # Ansible inventory
│   └── host_vars/
│       └── node1hp.yml          # Host-specific variables
├── README.md
```

## 🚀 Deployment

This project assumes:
- A local server (e.g. a thin client)
- Docker + Docker Compose installed
- Umami exposed through a secure Cloudflare Tunnel
- monitoring.codemining.dev DNS already set up

### Step 1 – Deploy the tunnel (Ansible)

Use the provided playbook to install and configure cloudflared and connect your local machine to the Cloudflare tunnel:
```bash
ansible-playbook playbooks/configure-cloudflared.yml -i inventory/hosts.ini
```

Requires a valid Cloudflare tunnel_id and credentials file in files/.

### Step 2 - Run Umami on server

```bash
cd docker
docker compose up -d
```

Umami instance will be available at:
[monitoring.codemining.dev](https://monitoring.codemining.dev)

## 🛣️ Roadmap

- [x] Manual deployment with Docker Compose
- [x] Secure tunnel via Cloudflared
- [x] Monitoring for https://hihi-bomba.codemining.dev
- [ ] Automatic deployment with FluxCD
- [ ] K3s cluster managed via Ansible
- [ ] Store secrets via SOPS or Sealed Secrets
- [ ] Add GitHub Actions workflow to build/test config
- [ ] Add dashboards for monitoring (Grafana/Loki?)

## 🧠 Motivation
This project is part of a broader educational DevOps journey to:
- Learn and apply GitOps practices
- Understand Kubernetes and Flux in real-world projects
- Host and monitor personal/family projects on local infrastructure
- Automate provisioning with reusable Ansible roles

Feel free to fork, contribute, or follow the progress
