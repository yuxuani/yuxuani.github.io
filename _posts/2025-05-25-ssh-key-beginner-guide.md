---
layout: post
title: "Complete SSH Guide for Beginners: Generating, Naming and Mananing SSH Keys."
seo_title: "How to generate and manage multiple SSH keys beginner guide"
description: “Everything you need to know about generating, naming, and managing SSH keys.”
date: 2025-05-25
tags: [git, github, ssh]
categories:
- Version Control
---
## 1. What is an SSH Key?

An SSH key is a pair of encrypted keys (public and private) used for secure remote login and authentication. Compared to passwords, SSH keys are more secure and easier to automate.

---

## 2. How to Generate an SSH Key?

Here’s how to generate the recommended key type `ed25519`, which works on most systems (Windows, macOS, Linux).

Open your terminal or command prompt and run:

```bash
ssh-keygen -t ed25519 -C "example@example.com" -f ~/.ssh/id_ed25519_example
```

Explanation:

- `-t ed25519`: specifies the ed25519 key type  
- `-C`: adds a comment to help identify the key (e.g., email, name, or any text)  
- `-f`: sets the file name to avoid overwriting default keys  

Follow the prompts and optionally set a passphrase. Two files will be created:

- Private key: `id_ed25519_example` — keep this safe and never share  
- Public key: `id_ed25519_example.pub` — can be shared and added to servers or platforms like GitHub  

---

## 3. How to View and Copy Your Public Key?

Your public key is in the `.pub` file. Use this command to display it:

```bash
cat ~/.ssh/id_ed25519_example.pub
```

Copy the entire output and paste it where your public key is needed, for example, in GitHub under SSH keys.

Note:
There are also other ways to view the ssh keys
- with scrolling `less ~/.ssh/id_ed25519_example.pub`
- using text editor `vim ~/.ssh/id_ed25519_example.pub` or `code ~/.ssh/id_ed25519_example.pub`
- or open the file manually
  - Windows: `C:\Users\<YourUsername>\.ssh\`
  - macOS/Linux: `~/.ssh/`

---

## 4. Adding SSH Key to GitHub

1. Log in to your GitHub account.  
2. Click your profile photo (top-right) → **Settings**.  
3. In the left menu, select **SSH and GPG keys**.  
4. Click the green **New SSH key** or **Add SSH key** button.  
5. Enter a descriptive title (e.g., “Laptop key” or “Work PC”).  
6. Paste your copied public key into the **Key** field.  
7. Click **Add SSH key** to save.  

Now you can interact with GitHub via SSH without typing your password.

---

## 5. How to Specify the SSH Key Filename?

When generating a key, you can use the `-f` option to set a custom filename, for example:

```bash
ssh-keygen -t ed25519 -C "example@example.com" -f ~/.ssh/id_ed25519_work
```

This creates `id_ed25519_work` and `id_ed25519_work.pub`, making it easier to manage multiple keys.

---

## 6. Managing Multiple SSH Keys and Accounts (e.g. GitHub & Servers)

If you have multiple GitHub accounts or different servers, manage them via the SSH config file `~/.ssh/config`.

Suppose you have three keys:

- `~/.ssh/id_ed25519_personal` — personal GitHub  
- `~/.ssh/id_ed25519_work` — work GitHub  
- `~/.ssh/id_ed25519_server` — remote server  

Create or edit `~/.ssh/config` and add:

```ssh-config
# Personal GitHub account
Host github-personal
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_personal

# Work GitHub account
Host github-work
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_work

# Remote Server
Host my-server
  HostName your.server.com
  User yourusername
  IdentityFile ~/.ssh/id_ed25519_server
```

Usage examples:

- For personal GitHub repo:

  ```
  git@github-personal:username/repo.git
  ```

- For work GitHub repo:

  ```
  git@github-work:username/repo.git
  ```

- SSH login to server:

  ```
  ssh my-server
  ```

This lets you use different keys for different accounts and servers without confusion.

---

## 8. Summary

- Use ed25519 keys by default for better security and speed  
- Use `-f` to specify filenames and manage multiple keys easily  
- Configure `~/.ssh/config` to handle multiple keys and hosts smoothly  
- Copy the `.pub` file content to GitHub or servers to enable access  
- Add meaningful comments to identify keys easily  

This beginner’s guide should help you quickly start with SSH keys and manage them effectively!

