# Bootstrap Cluster with Ansible

An [Ansible](https://www.ansible.com/) repository for personalizing server clusters and ensuring a consistent base environment across all nodes. This repository serves as a foundational layer for server-specific customizations in development, staging, and production environments.

Initially focused on Debian/Ubuntu, with plans to support additional operating systems in the future.

## ✨ Features

- Sync timezone & NTP
- Packages update/install (apt)
  - nano, git, curl
  - qemu-guest-agent for qemu VM
- Shell with zsh and [starship](https://github.com/starship/starship)
- ...

## ✅ Requirements

### 💻 Control Machine

- Ansible >= 2.11 (tested on 2.17.3)

  Install the latest version of Ansible using [pipx](https://github.com/pypa/pipx):

  ```shell
  $ pipx install --include-deps ansible
  ```

### 🖧 Managed Nodes

- Debian/Ubuntu (tested on Ubuntu 24.04 Minimal)

  Can be bare-metal, virtual machine, or even docker container.

## 🏃‍♂️‍➡️ Getting Started

### ⏱️ Preparation

Clone this repository:

```shell
git clone https://github.com/OoadadaoO/cluster-bootstrap-ansible
cd cluster-bootstrap-ansible
```

Install Ansible collections:

```shell
ansible-galaxy collection install -r collections/requirements.yml
```

### ⚙️ Configuration

Copy the example files:

```shell
cp production.example production # staging inventory
cp staging.example staging # production inventory
cp ansible.example.cfg ansible.cfg # ansible pre configuration
cp group_vars/all.example.yml group_vars/all.yml # all variables
```

Update the inventory `production` or `staging` with your server's IP/hostname.

Configure the variables in `group_vars/all.yml` with your preferences.

_(Optional)_ Specific variable configurations.

- `group_vars/production.yml`: for production inventory
- `group_vars/staging.yml`: for staging inventory
- `group_vars/<group>.yml`: for specific group
- `host_vars/<host>.yml`: for specific host

### 🪄 Ansible Magic

```shell
# for staging inventory
ansible-playbook -i staging site.yml

# for production inventory
ansible-playbook -i production site.yml
```
