## ✅ Recommended Ansible Collections

### 🔧 **1. `community.general`**

* **Purpose**: Contains a wide variety of general-purpose modules and plugins.
* **Useful For**: File manipulation, cron, user management, services, etc.
* **Install**:

  ```bash
  ansible-galaxy collection install community.general
  ```
* **Example**:

  ```yaml
  - name: Add a cron job
    community.general.cron:
      name: "logrotate"
      job: "/usr/sbin/logrotate"
      minute: "0"
      hour: "1"
  ```

---

### ☁️ **2. `amazon.aws`**

* **Purpose**: AWS modules and plugins for EC2, VPC, S3, IAM, etc.
* **Install**:

  ```bash
  ansible-galaxy collection install amazon.aws
  ```
* **Example**:

  ```yaml
  - name: Create an EC2 instance
    amazon.aws.ec2_instance:
      name: web1
      key_name: mykey
      instance_type: t2.micro
      image_id: ami-0abcdef1234567890
      wait: yes
      region: us-east-1
  ```

---

### ☁️ **3. `azure.azcollection`**

* **Purpose**: Azure resource management.
* **Install**:

  ```bash
  ansible-galaxy collection install azure.azcollection
  ```
* **Example**:

  ```yaml
  - name: Create a resource group
    azure.azcollection.azure_rm_resourcegroup:
      name: myResourceGroup
      location: eastus
  ```

---

### 🔒 **4. `ansible.posix`**

* **Purpose**: POSIX-compliant system tools.
* **Use for**: SELinux, file permissions, mount points, etc.
* **Install**:

  ```bash
  ansible-galaxy collection install ansible.posix
  ```
* **Example**:

  ```yaml
  - name: Set SELinux mode
    ansible.posix.selinux:
      policy: targeted
      state: permissive
  ```

---

### 🔄 **5. `community.docker`**

* **Purpose**: Manage Docker containers, images, and networks.
* **Install**:

  ```bash
  ansible-galaxy collection install community.docker
  ```
* **Example**:

  ```yaml
  - name: Run a Docker container
    community.docker.docker_container:
      name: nginx
      image: nginx:latest
      state: started
      ports:
        - "80:80"
  ```

---

### 📦 **6. `community.mysql`**

* **Purpose**: Manage MySQL databases, users, and schemas.
* **Install**:

  ```bash
  ansible-galaxy collection install community.mysql
  ```
* **Example**:

  ```yaml
  - name: Create database and user
    community.mysql.mysql_user:
      name: devuser
      password: secret
      priv: 'mydb.*:ALL'
      state: present
  ```

---

### 📚 **7. `ansible.builtin`** (built-in modules)

* Comes preinstalled with Ansible.
* Always use **fully qualified names** for clarity and best practice:

  ```yaml
  ansible.builtin.copy
  ansible.builtin.replace
  ansible.builtin.service
  ```

---

## 🧰 Community Roles (Examples from Galaxy)

### 🖥️ **geerlingguy.apache**

* Set up Apache web server.

```bash
ansible-galaxy role install geerlingguy.apache
```

### 🧪 **geerlingguy.docker**

* Install and configure Docker engine.

```bash
ansible-galaxy role install geerlingguy.docker
```

### 📦 **geerlingguy.mysql**

* Set up and manage MySQL.

```bash
ansible-galaxy role install geerlingguy.mysql
```

---

## 📄 Example `requirements.yml`

```yaml
---
collections:
  - name: community.general
  - name: amazon.aws
  - name: azure.azcollection
  - name: ansible.posix
  - name: community.docker
  - name: community.mysql

roles:
  - name: geerlingguy.apache
  - name: geerlingguy.docker
  - name: geerlingguy.mysql
```

**Install all:**

```bash
ansible-galaxy install -r requirements.yml
```

---
