# Secure Linux User Management Automation

## Overview

This repository contains a **production-grade Bash script** that automates secure Linux user management using **security best practices** and the **principle of least privilege**.

It is designed to replace insecure defaults (root login, password authentication) with a hardened configuration suitable for **cloud servers, DevOps pipelines, and production systems**.

---

## Key Features

- Creates a **non-root administrative user**
- Configures **least-privilege sudo access**
- Enforces **SSH key-only authentication**
- Disables **password-based login**
- Disables **direct root SSH access**

---

## Why This Project Matters

This project demonstrates:

- 🔐 Security-first system design
- 🛡️ Protection against brute-force attacks
- 🔑 Proper SSH key management
- 🚫 Elimination of root-level exposure
- 🧠 Real-world Linux administration practices

These are standard requirements in:
- Cloud infrastructure (AWS, GCP, Azure)
- SOC2 / CIS-compliant environments
- DevOps & SRE roles
- Production Linux servers

---

## Script Workflow

1. Creates a non-root admin user (`devopsadmin`)
2. Grants sudo access via `/etc/sudoers.d/`
3. Configures secure SSH permissions
4. Enforces SSH key authentication
5. Locks password-based access
6. Disables root SSH login
7. Restarts SSH service safely

---

## Prerequisites

- Linux system with `systemd`
- OpenSSH installed
- Root or sudo access

---

## Usage

```bash
chmod +x secure_admin_setup.sh
sudo ./secure_admin_setup.sh
