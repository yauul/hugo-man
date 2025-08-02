---

title: "How to Use SSH Keys for Secure Login"
date: 2025-07-26T11:00:00+03:00
description: "Learn how to generate and use SSH keys for passwordless login to Linux servers."
tags: ["ssh", "linux", "security", "ssh-keys"]
series: ["Linux Admin"]
series_order: 2

---

SSH keys are a secure and convenient way to log into remote servers without typing passwords.

## Step 1: Generate SSH Key Pair

On your local machine:

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

- Press Enter to accept default file path (usually `~/.ssh/id_rsa`)
- Set a passphrase for added security (optional)

## Step 2: Copy Public Key to Server

```bash
ssh-copy-id user@remote_host
```

Or manually copy the contents of `~/.ssh/id_rsa.pub` to `~/.ssh/authorized_keys` on the server.

![TEST@](test2.jpg "a title")


## Step 3: Test SSH Login

```bash
ssh user@remote_host
```

You should now be logged in without entering a password.

## Optional: Disable Password Authentication

On the remote server:

1. Edit SSH config:

```bash
sudo nano /etc/ssh/sshd_config
```

2. Set:
```bash
PasswordAuthentication no
```

3. Restart SSH:
```bash
sudo systemctl restart sshd
```

## You're All Set!

SSH keys make logging into servers easier and more secure. Protect your private key and use passphrases when possible.