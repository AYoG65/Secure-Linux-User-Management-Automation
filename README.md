# Secure Linux User Management Automation

A production-grade Bash script that automates secure Linux user provisioning using the principle of least privilege. Built for cloud servers, DevOps pipelines, and any environment where root access needs to be locked down from day one.

---

## The Problem

Fresh Linux servers are insecure by default. Root login is often enabled, password authentication is active, and there's no separation between administrative and service accounts. In cloud and enterprise environments — where servers are provisioned at scale — manual hardening is slow, inconsistent, and error-prone.

This script solves that by automating the secure baseline in a single, idempotent run.

---

## What It Does

| Step | Action |
|---|---|
| 1 | Creates a named non-root admin user (`devopsadmin`) |
| 2 | Grants least-privilege sudo access via `/etc/sudoers.d/` |
| 3 | Configures correct SSH key permissions (`~/.ssh`, `authorized_keys`) |
| 4 | Enforces SSH key-only authentication |
| 5 | Disables password-based SSH login |
| 6 | Disables direct root SSH access |
| 7 | Restarts SSH service safely to apply changes |

---

## Why This Matters

These controls are standard requirements in:

- **CIS Benchmark Level 1** hardened environments
- **SOC 2 compliant** infrastructure
- **Cloud server provisioning** (AWS EC2, Azure VM, GCP Compute)
- **DevOps / SRE** production Linux systems
- Any environment running automated MDM or configuration management

Eliminating password-based login and root SSH access removes the two most common attack vectors for brute-force and credential-stuffing attacks against exposed Linux hosts.

---

## Usage

```bash
chmod +x Secure_Admin_Setup
sudo ./Secure_Admin_Setup
```

The script is **idempotent** — safe to run multiple times without creating duplicate users or breaking existing configuration.

---

## Sample Output

```
[*] Creating admin user: devopsadmin
[*] Granting sudo access via /etc/sudoers.d/devopsadmin
[*] Setting up SSH directory and permissions
[*] Configuring SSH: disabling password authentication
[*] Configuring SSH: disabling root login
[*] Restarting SSH service
[✓] Secure user setup complete.
[✓] Login as devopsadmin using your SSH key. Root SSH is now disabled.
```

---

## Security Controls Applied

- **No root login** — `PermitRootLogin no` enforced in `sshd_config`
- **No password auth** — `PasswordAuthentication no` enforced
- **SSH key-only** — access requires a pre-configured authorized key
- **Least privilege sudo** — admin user has sudo rights without becoming root by default
- **Correct file permissions** — `.ssh/` set to `700`, `authorized_keys` set to `600`

---

## Supported Platforms

- Ubuntu 20.04 / 22.04 / 24.04
- Debian 11 / 12
- RHEL 8 / 9
- Any Linux system with `systemd` and OpenSSH installed

---

## Repository Structure

```
Secure-Linux-User-Management-Automation/
├── Secure_Admin_Setup     # Main provisioning script
├── docs/                  # Additional documentation
├── .gitignore
├── LICENSE
└── README.md
```

---

## Real-World Context

This pattern is the baseline for any cloud VM that gets deployed in a production pipeline. Whether you're provisioning via Terraform, Ansible, or a cloud-init script, the underlying SSH hardening looks exactly like this. Writing it as a standalone script makes it testable, auditable, and easy to slot into any automation workflow.

---

## Future Enhancements

- Parameterize the admin username (currently hardcoded as `devopsadmin`)
- Add support for multiple authorized SSH keys
- Wrap as an Ansible role for fleet-wide deployment
- Add audit logging for all changes made
- Add optional fail2ban installation for brute-force protection

---

## Topics

`linux` `bash` `security` `ssh-hardening` `user-management` `automation` `sysadmin` `devops` `cis-benchmark` `cloud`
