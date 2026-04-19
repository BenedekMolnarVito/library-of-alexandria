---
title: "Hobby Server"
type: entity
domain: personal
tags:
  - infrastructure
  - self-hosting
  - docker
  - server
  - homelab
created: 2026-04-19
updated: 2026-04-19
sources:
  - "[[sources/personal-vault-init-prompt]]"
---

# Hobby Server

A self-hosted server running on an old HP laptop, used by [[wiki/entities/molnar-benedek]] for hosting personal projects, testing, and learning about server management and networking.

## Configuration

| Property | Value |
|----------|-------|
| **Domain** | vitoscaletta.duckdns.org |
| **DNS Provider** | DuckDNS |
| **Reverse Proxy** | nginx |
| **Container Runtime** | Docker |
| **Storage** | 4TB NAS drive (mounted) |
| **Hardware** | Old HP laptop |

## SSH Access

| Property | Value |
|----------|-------|
| **LAN IP** | 192.168.100.4 |
| **Port** | 22 |
| **Username** | *(ask user — not stored for security)* |
| **Password** | *(ask user — not stored for security)* |

> [!warning] Security Note
> SSH credentials are intentionally not stored in this vault. When an agent needs to SSH into the hobby server, it should prompt the user for username and password.

## Purpose

- Hosting small web applications for learning and experimentation
- File storage and media management (4TB NAS)
- Backup management
- Learning server administration and networking
- Docker container experimentation

## Related Concepts

- [[wiki/concepts/self-hosting]]
- [[wiki/concepts/software-engineering]]
