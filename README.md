Ansible Paperless Stack (Techno Tim Style)

Deploys a full Paperless-ngx Docker Compose stack with optional local AI services using a clean, role-based Ansible structure.

⸻

🚀 What This Role Deploys

Core Services
	•	Paperless-ngx
	•	PostgreSQL
	•	Redis
	•	Gotenberg
	•	Apache Tika

Optional Services (Compose Profiles)
	•	Ollama (local LLM)
	•	Open WebUI
	•	Paperless-AI
	•	Paperless-GPT
	•	Dozzle (container log viewer)

⸻

🏗 Repository Structure

ansible-paperless-stack/
├── site.yml
├── inventories/
│   └── lab/
│       ├── hosts.ini
│       └── group_vars/
│           └── paperless.yml
└── roles/
    └── paperless_stack/
        ├── defaults/
        ├── tasks/
        ├── templates/
        └── meta/


⸻

⚙️ Requirements

Target host:
	•	Debian / Ubuntu
	•	Docker + docker-compose-plugin (installed automatically by role)

Controller:
	•	Ansible 2.15+

⸻

🧪 Quick Start

1️⃣ Run with core services only

ansible-playbook -i inventories/lab/hosts.ini site.yml

2️⃣ Enable AI services

ansible-playbook -i inventories/lab/hosts.ini site.yml \
  -e paperless_enable_ai=true

3️⃣ Enable Dozzle

ansible-playbook -i inventories/lab/hosts.ini site.yml \
  -e paperless_enable_dozzle=true


⸻

🔐 Secrets Handling

The PostgreSQL password is:
	•	Generated once on the Ansible controller
	•	Stored in:

.secrets/<inventory_hostname>.paperless.dbpass

This ensures:
	•	Idempotency
	•	No password regeneration on re-runs
	•	Safe snapshot restores

⚠️ Do NOT commit the .secrets/ directory.

⸻

🔑 Paperless API Token (Required for AI Services)

If enabling AI services:
	1.	Deploy stack normally
	2.	Log into Paperless web UI
	3.	Go to Profile → API Tokens
	4.	Create a token
	5.	Set in:

inventories/lab/group_vars/paperless.yml

paperless_api_token: "YOUR_TOKEN_HERE"

	6.	Re-run playbook with paperless_enable_ai=true

⸻

🌐 Default Service URLs

Service	URL
Paperless	http://SERVER:8000
Dozzle	http://SERVER:8080
Open WebUI	http://SERVER:3001
Paperless-AI	http://SERVER:3000
Paperless-GPT	http://SERVER:3002


⸻

🧠 Design Philosophy

This role is structured to be:
	•	Modular
	•	Idempotent
	•	Profile-based (AI optional)
	•	Controller-secret-safe
	•	Git-friendly

It is intended to be reusable across:
	•	Homelab environments
	•	Dev/Test
	•	Production

⸻

🛠 Future Enhancements

Possible improvements:
	•	Reverse proxy integration (Traefik / Nginx Proxy Manager)
	•	Automated backups
	•	Health checks
	•	Watchtower integration
	•	GPU role for NVIDIA support
	•	Molecule testing

⸻

📜 License

MIT License

⸻

Built for clean infrastructure automation and long-term maintainability.
