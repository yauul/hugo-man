---
title: "How to Deploy Pi-hole on Your Network"
date: 2025-07-26T10:00:00+03:00
description: "Step-by-step guide to deploying Pi-hole to block ads and trackers on your home network."
tags: ["pi-hole", "dns", "ad-blocking", "linux"]
---

Pi-hole is a powerful DNS-level ad blocker that improves network performance and privacy. This guide walks you through deploying Pi-hole on a Linux server or Raspberry Pi.

## Prerequisites

- A Linux-based system (Debian, Ubuntu, or Raspberry Pi OS)
- Static IP address
- Root or sudo privileges

## Step 1: Update Your System

```bash
sudo apt update && sudo apt upgrade -y
```

## Step 2: Install Pi-hole

Run the automated install script:

```bash
curl -sSL https://install.pi-hole.net | bash
```

Follow the prompts to:
- Choose an interface
- Select an upstream DNS provider (like Cloudflare or Google DNS)
- Enable web admin interface

## Step 3: Configure Your Router

Point your router’s DNS to the Pi-hole IP address so all devices use it:

- Access your router admin page
- Set primary DNS to your Pi-hole’s static IP

## Step 4: Access the Admin Dashboard

Visit:
```
http://<PI-HOLE-IP>/admin
```

Use the password provided at the end of installation (or reset it with `pihole -a -p`).

## Optional: Secure with SSL and Passwords

Consider using a reverse proxy (e.g., NGINX) with HTTPS and basic auth for remote access.

## That’s It!

You now have network-wide ad blocking with minimal setup. Enjoy a cleaner, faster internet!
