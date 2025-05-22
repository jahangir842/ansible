### 📦 What is Ansible Galaxy?

**Ansible Galaxy** is the **official community hub** for finding, sharing, and downloading **Ansible roles and collections**. It allows users to **reuse automation content** written by others and **publish** their own roles/collections for others to use.

---

### 🔍 Key Concepts

#### 1. **Roles**

Roles in Ansible are a way of **organizing playbooks** into reusable components. They contain tasks, handlers, variables, templates, and other files in a structured way.

* A role might manage a service like `nginx`, `mysql`, or set up a base server configuration.

Example:

```bash
ansible-galaxy init my_nginx_role
```

Creates a role directory structure:

```
my_nginx_role/
├── defaults/
├── files/
├── handlers/
├── meta/
├── tasks/
├── templates/
├── tests/
└── vars/
```

#### 2. **Collections**

Collections are a distribution format that **bundles roles, modules, plugins, and playbooks** together. This is a more **modern** and **scalable** way to distribute automation content compared to roles alone.

* Example: `community.general`, `ansible.posix`, `amazon.aws`

```bash
ansible-galaxy collection install community.general
```

---

### 🎯 What Can You Do With Ansible Galaxy?

* **Find** roles and collections by other users or vendors.
* **Install** them using the `ansible-galaxy` command-line tool.
* **Share** your own content with the community.
* **Automate** without rewriting everything from scratch.

---

### 📁 Ansible Galaxy CLI Commands

#### 1. **Installing a Role**

```bash
ansible-galaxy role install geerlingguy.mysql
```

This installs the `mysql` role by user `geerlingguy`.

#### 2. **Installing a Collection**

```bash
ansible-galaxy collection install ansible.posix
```

#### 3. **Creating a Role Scaffold**

```bash
ansible-galaxy init my_custom_role
```

#### 4. **Creating a Collection Scaffold**

```bash
ansible-galaxy collection init my_namespace.my_collection
```

#### 5. **Listing Installed Collections**

```bash
ansible-galaxy collection list
```

#### 6. **Removing a Collection**

```bash
ansible-galaxy collection uninstall ansible.posix
```

---

### 🏷️ Galaxy Requirements File

You can manage dependencies using a `requirements.yml` file.

**Example:**

```yaml
---
roles:
  - name: geerlingguy.nginx

collections:
  - name: community.general
  - name: amazon.aws
```

**Install all with:**

```bash
ansible-galaxy install -r requirements.yml
```

---

### 🔐 Sources of Roles and Collections

* [https://galaxy.ansible.com](https://galaxy.ansible.com)
* GitHub or private Git repositories (by specifying URLs)
* Automation Hub (for Red Hat Ansible Automation Platform)

---

### 🧩 Use Case Examples

#### Use Case 1: Installing and Using a Role

```bash
ansible-galaxy role install geerlingguy.apache
```

```yaml
# playbook.yml
- hosts: web
  roles:
    - geerlingguy.apache
```

#### Use Case 2: Installing a Collection and Using Its Modules

```bash
ansible-galaxy collection install community.mysql
```

```yaml
# playbook.yml
- hosts: db
  tasks:
    - name: Create a MySQL database
      community.mysql.mysql_db:
        name: mydb
        state: present
        login_user: root
        login_password: root_pass
```

---

### 🧰 Best Practices

* Pin versions in `requirements.yml` to avoid breaking changes:

```yaml
collections:
  - name: community.general
    version: ">=3.0.0,<4.0.0"
```

* Use fully-qualified module names when working with collections (e.g., `community.mysql.mysql_db` instead of `mysql_db`).

* Test third-party content in a non-production environment.

---

### 🚀 Summary

| Feature              | Description                                       |
| -------------------- | ------------------------------------------------- |
| **Galaxy Website**   | GUI to browse roles and collections               |
| **CLI Tool**         | `ansible-galaxy` for managing content             |
| **Roles**            | Structured, reusable units of automation          |
| **Collections**      | Bundled automation content (roles, plugins, etc.) |
| **requirements.yml** | Define and manage dependencies for reuse          |

---
