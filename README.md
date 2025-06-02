# 🛠️ Ansible Practice Repository

Welcome to the **Ansible Practice Repository**.
This repository is designed as a hands-on environment to learn, test, and refine skills related to Ansible concepts, modules, playbooks, and automation best practices.

---

## 📌 Example Usage

```bash
ansible-playbook -i ~/projects/ansible/inventories/inventory.yml install_vlc.yml -K
```

---

## Prepare New Client Node

### Enable SSH Password Authentication (Manual)

1. Edit SSH config:

   ```bash
   sudo nano /etc/ssh/sshd_config
   ```
2. Change:

   ```bash
   #PasswordAuthentication no
   ```

   to

   ```bash
   PasswordAuthentication yes
   ```
3. Save and exit, then restart SSH:

   ```bash
   sudo systemctl restart ssh
   ```

> **Note:** Enabling password authentication increases security risks. Use strong passwords and consider additional protections like fail2ban.

---

### Allow SSH through firewalld

```bash
sudo firewall-cmd --permanent --add-service=ssh
sudo firewall-cmd --reload
```

---

### Configure Passwordless `sudo` (Optional)

1. Edit sudoers:

   ```bash
   sudo visudo
   ```
2. Add:

   ```bash
   userid ALL=(ALL) NOPASSWD:ALL
   ```

> **Warning:** Use carefully due to security implications.

---

## 🔐 Running with Elevated Privileges

To allow Ansible to prompt for your `sudo` password when executing tasks requiring privilege escalation, append the `--ask-become-pass` (`-K`) flag:

```bash
ansible-playbook ./playbooks/ubuntu/installation/install_vim.yml -K
```

### 🔓 Configure Passwordless `sudo` (Optional)

To avoid password prompts entirely, configure passwordless `sudo` for your user:

```bash
sudo visudo
```


Then add the following line (replace `jahangir` with your actual username):

```bash
jahangir ALL=(ALL) NOPASSWD:ALL
```

> ⚠️ Use with caution; this has security implications in multi-user or production environments.

---

## 🚀 Getting Started with Ansible

If you're new to Ansible, consider exploring the official documentation:

### 📘 Core Concepts

* [Getting Started Guide](https://docs.ansible.com/ansible/latest/getting_started/index.html)

### ⚙️ Setup & Configuration

* [Installation Guide](https://docs.ansible.com/ansible/latest/installation_guide/index.html)
* [Intro to Configuration](https://docs.ansible.com/ansible/latest/installation_guide/intro_configuration.html)

### 📂 Inventory Management

* [Inventory Guide](https://docs.ansible.com/ansible/latest/inventory_guide/index.html)

### 📜 Playbooks

* [Playbook Guide](https://docs.ansible.com/ansible/latest/playbook_guide/index.html)

### 🔐 Secrets & Vault

* [Vault Guide](https://docs.ansible.com/ansible/latest/vault_guide/index.html)

### 💻 CLI Usage

* [Command-Line Guide](https://docs.ansible.com/ansible/latest/command_guide/index.html)

### 🔌 Modules & Plugins

* [Module and Plugin Guide](https://docs.ansible.com/ansible/latest/module_plugin_guide/index.html)

### 🌌 Ansible Galaxy

* [Galaxy User Guide](https://docs.ansible.com/ansible/latest/galaxy/user_guide.html)

---

## 📁 Repository Structure (Work in Progress)

```bash
.
├── inventory/               # Custom inventory files
├── playbooks/              # Main playbooks for experimentation
├── roles/                  # Role-based structure following best practices
├── vault/                  # Vault-encrypted secrets
├── configs/                # Custom configuration files (e.g., ansible.cfg)
└── README.md               # Project documentation
```

---

## 🎯 Practice Topics

This repository includes or will include examples for the following Ansible practices:

* Working with core modules like `ansible.builtin.ping`, `ansible.builtin.copy`, and `ansible.builtin.command`
* Creating and managing both static and dynamic inventory files
* Writing idempotent and modular playbooks
* Encrypting sensitive data with Ansible Vault
* Using tags, handlers, conditionals, and loops
* Creating and consuming Ansible roles
* Integrating community roles via `ansible-galaxy`

---

## 📝 Notes

This is an ongoing learning project. Planned future enhancements include:

* Expanded playbook and role examples
* Real-world automation scenarios
* Role-based architecture for modular deployments
* Infrastructure provisioning (including cloud platforms)

You are welcome to fork or clone this repository and follow along with your own practice.

---

## 📬 Feedback & Contributions

Contributions, ideas, and suggestions are welcome!
Please feel free to open an issue or submit a pull request.

Happy Automating! ⚙️

---

