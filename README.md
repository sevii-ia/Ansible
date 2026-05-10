# Ansible

Configuration Ansible repository for automating Linux and Windows host setup.

## Features

- Linux package installation with `apt`
- Windows software installation with Chocolatey
- Windows connectivity check using `win_ping`
- OS-based software installation for Linux and Windows
- Nginx default page text replacement
- Custom Ansible configuration via `ansible.cfg`

## Repository Structure

```text
Ansible/
├── hosts/
│   ├── all
│   ├── linux
│   └── windows
├── playbook/
│   ├── install-linux.yaml
│   ├── install-soft-windows.yaml
│   ├── install-windows-linux.yaml
│   ├── page.yaml
│   └── ping-pong.yaml
├── ConfigureRemotingForAnsible
├── ansible.cfg
├── install_ansible.sh
├── LICENSE
└── README.md
````

## Requirements

* Ansible
* Python 3
* SSH access for Linux hosts
* WinRM configured for Windows hosts
* Chocolatey installed on Windows hosts
* `sudo` privileges for Linux package installation

## Installation

Clone the repository:

```bash
git clone https://github.com/sevii-ia/Ansible.git
cd Ansible
```

Install Ansible on Ubuntu/Debian:

```bash
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```

## Configuration

Edit inventory files in the `hosts/` directory before running playbooks.

Example inventory usage:

```bash
ansible-playbook -i hosts/all playbook/ping-pong.yaml
```

> Do not store plaintext passwords in inventory files. Use Ansible Vault or SSH keys where possible.

## Usage

### Test Windows connectivity

```bash
ansible-playbook -i hosts/windows playbook/ping-pong.yaml
```

### Install software on Linux

Installs `mc`:

```bash
ansible-playbook -i hosts/linux playbook/install-linux.yaml
```

### Install software on Windows

Installs Firefox using Chocolatey:

```bash
ansible-playbook -i hosts/windows playbook/install-soft-windows.yaml
```

### Install software based on OS

Installs Linux packages on Debian-based systems and Windows software on Windows hosts:

```bash
ansible-playbook -i hosts/all playbook/install-windows-linux.yaml
```

### Replace Nginx welcome page text

```bash
ansible-playbook -i hosts/linux playbook/page.yaml
```

## Playbooks

| Playbook                     | Description                                 |
| ---------------------------- | ------------------------------------------- |
| `ping-pong.yaml`             | Tests Windows connectivity with `win_ping`  |
| `install-linux.yaml`         | Installs `mc` on Linux hosts                |
| `install-soft-windows.yaml`  | Installs Firefox on Windows hosts           |
| `install-windows-linux.yaml` | Installs software depending on detected OS  |
| `page.yaml`                  | Replaces text in `/var/www/html/index.html` |

## Troubleshooting

Check inventory connectivity:

```bash
ansible all -i hosts/all -m ping
```

For Windows hosts:

```bash
ansible windows -i hosts/windows -m win_ping
```

Common issues:

* Incorrect host IP address
* SSH or WinRM not enabled
* Invalid credentials
* Missing sudo privileges
* Chocolatey not installed on Windows

## Security Notes

This repository contains inventory-style host configuration. Avoid committing real passwords, private IPs, or sensitive credentials. Recommended options:

```bash
ansible-vault encrypt hosts/all
```

or use SSH keys and external secrets management.

## License

This project is licensed under the MIT License.

See the [LICENSE](LICENSE) file for more information.
