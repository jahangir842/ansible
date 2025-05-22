The [**ansible-lockdown**](https://github.com/ansible-lockdown) project by *Ansible-Lockdown* (part of MindPoint Group) provides **Ansible roles** to enforce security baselines for various operating systems and applications, aligned with compliance benchmarks like **CIS** (Center for Internet Security), **DISA STIG**, and more.

Here’s an overview of commonly used roles for **RHEL**, **Ubuntu**, and **Windows**:

---

### 🔐 RHEL (Red Hat Enterprise Linux)

| Role                                                         | Description                             | Benchmark |
| ------------------------------------------------------------ | --------------------------------------- | --------- |
| [`RHEL8-CIS`](https://github.com/ansible-lockdown/RHEL8-CIS) | Hardens RHEL 8 systems to CIS Benchmark | CIS       |
| [`RHEL7-CIS`](https://github.com/ansible-lockdown/RHEL7-CIS) | Hardens RHEL 7 systems to CIS Benchmark | CIS       |
| [`RHEL9-CIS`](https://github.com/ansible-lockdown/RHEL9-CIS) | For RHEL 9 systems                      | CIS       |

#### Example usage (RHEL 8):

```yaml
- name: Harden RHEL 8 using CIS Benchmark
  hosts: all
  become: true
  roles:
    - role: ansible-lockdown.rhel8_cis
```

---

### 🛡️ Ubuntu

| Role                                                                   | Description                    | Benchmark |
| ---------------------------------------------------------------------- | ------------------------------ | --------- |
| [`Ubuntu2004-CIS`](https://github.com/ansible-lockdown/UBUNTU2004-CIS) | CIS Benchmark for Ubuntu 20.04 | CIS       |
| [`Ubuntu2204-CIS`](https://github.com/ansible-lockdown/UBUNTU2204-CIS) | CIS Benchmark for Ubuntu 22.04 | CIS       |

#### Example usage (Ubuntu 22.04):

```yaml
- name: Harden Ubuntu 22.04 using CIS Benchmark
  hosts: all
  become: true
  roles:
    - role: ansible-lockdown.ubuntu2204_cis
```

---

### 🪟 Windows

| Role                                                                       | Description                           | Benchmark |
| -------------------------------------------------------------------------- | ------------------------------------- | --------- |
| [`Windows-2019-CIS`](https://github.com/ansible-lockdown/Windows-2019-CIS) | CIS Benchmark for Windows Server 2019 | CIS       |
| [`Windows-2016-CIS`](https://github.com/ansible-lockdown/Windows-2016-CIS) | CIS Benchmark for Windows Server 2016 | CIS       |
| [`Windows-2022-CIS`](https://github.com/ansible-lockdown/Windows-2022-CIS) | CIS Benchmark for Windows Server 2022 | CIS       |

#### Example usage (Windows Server 2019):

```yaml
- name: Harden Windows Server 2019
  hosts: windows
  roles:
    - role: ansible-lockdown.windows_2019_cis
```

> **Note:** Windows roles require:
>
> * `ansible.windows` and `community.windows` collections.
> * WinRM connectivity set up.

---

### 🔧 How to Install a Role

```bash
ansible-galaxy install ansible-lockdown.rhel8_cis
ansible-galaxy install ansible-lockdown.ubuntu2204_cis
ansible-galaxy install ansible-lockdown.windows_2019_cis
```

---

### 📝 Configuration

Each role provides a `defaults/main.yml` and `vars/main.yml` file to configure:

* Compliance levels
* Skipping specific controls
* Audit only or apply mode

You can override them in your playbook or `group_vars`.

---

### ✅ Best Practices

* Run in **audit mode** first.
* Review findings and impact before enabling remediation.
* Use **tags** to limit scope (e.g., `--tags "level_1"`).
* Integrate with **CI/CD** or **configuration drift detection**.

---

Here’s a **multi-platform Ansible playbook** example that applies the correct `ansible-lockdown` role based on the target host's OS — covering **RHEL**, **Ubuntu**, and **Windows** systems. This playbook uses `ansible_facts` for conditional role inclusion.

---

### 🗂️ Directory structure (recommended)

```
site.yml
group_vars/
  all.yml
inventory/
  hosts.ini
```

---

### 🧠 `inventory/hosts.ini`

```ini
[rhel]
rhel1.example.com

[ubuntu]
ubuntu1.example.com

[windows]
win1.example.com ansible_user=Administrator ansible_password=SecretPass123 ansible_connection=winrm ansible_port=5986 ansible_winrm_transport=basic
```

---

### ⚙️ `group_vars/all.yml`

You can define baseline role variables here or override them per host.

```yaml
cis_level: 1
cis_audit_only: false
```

---

### ▶️ `site.yml` – Main Playbook

```yaml
- name: Apply CIS Hardening - Linux and Windows
  hosts: all
  gather_facts: true
  become: true
  tasks:
    - name: Include CIS role for RHEL 8
      ansible.builtin.include_role:
        name: ansible-lockdown.rhel8_cis
      when: ansible_facts['distribution'] == "RedHat" and ansible_facts['distribution_major_version'] == "8"

    - name: Include CIS role for Ubuntu 22.04
      ansible.builtin.include_role:
        name: ansible-lockdown.ubuntu2204_cis
      when: ansible_facts['distribution'] == "Ubuntu" and ansible_facts['distribution_version'] is search("22.04")

    - name: Include CIS role for Windows Server 2019
      ansible.builtin.include_role:
        name: ansible-lockdown.windows_2019_cis
      when: ansible_facts['os_family'] == 'Windows' and ansible_facts['os_version'] is search("10.0.17763")
```

---

### 📦 Install Required Roles

```bash
ansible-galaxy install \
  ansible-lockdown.rhel8_cis \
  ansible-lockdown.ubuntu2204_cis \
  ansible-lockdown.windows_2019_cis
```

Also install the required **collections**:

```bash
ansible-galaxy collection install \
  ansible.windows \
  community.windows
```

---

### 🧪 Run the playbook

```bash
ansible-playbook -i inventory/hosts.ini site.yml
```

---

### ✅ Tips

* Add `--check` for dry-run.
* Add `--tags "level_1"` to run specific levels.
* Each role supports audit mode using `cis_audit_only: true`.

---

