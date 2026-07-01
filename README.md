# YAY

[![CICD](https://github.com/jahrik/ansible-yay/actions/workflows/cicd.yml/badge.svg)](https://github.com/jahrik/ansible-yay/actions/workflows/cicd.yml)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-jahrik.yay-blue?logo=ansible)](https://galaxy.ansible.com/ui/standalone/roles/jahrik/yay/)

Installs [yay](https://github.com/Jguer/yay) — Yet Another Yogurt, an AUR helper for Arch Linux — and provides a `library/yay` Ansible module for installing AUR packages declaratively from other roles.

**Arch Linux only** — does not support Debian, macOS, or SteamOS.

## Role Variables

| Variable | Default | Description |
|---|---|---|
| `install` | `true` | Set to `false` to uninstall yay |
| `aur_packages` | `[]` | List of AUR packages to install after yay is set up |

## Example Playbook

Install yay and AUR packages:

```yaml
---
- hosts: all
  roles:
    - role: jahrik.yay
      vars:
        aur_packages:
          - polybar
          - hyprland
```

Install yay only:

```yaml
---
- hosts: all
  roles:
    - role: jahrik.yay
```

To uninstall:

```yaml
---
- hosts: all
  vars:
    install: false
  roles:
    - role: jahrik.yay
```

## Tags

Run or skip parts of the role with tags:

```bash
ansible-playbook playbook.yml --tags yay:install
ansible-playbook playbook.yml --skip-tags yay:uninstall
```

| Tag | Scope |
|---|---|
| `yay` | All role tasks |
| `yay:install` | Install path only |
| `yay:uninstall` | Uninstall path only |

## Testing

```bash
uv sync
source .venv/bin/activate
yamllint .
ansible-lint
molecule test
```

Step by step:

```bash
molecule converge
molecule verify
molecule destroy
```

## License

GPLv2

## Author Information

jahrik@gmail.com
