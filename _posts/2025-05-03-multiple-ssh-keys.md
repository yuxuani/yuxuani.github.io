---
layout: post
title: How to Use Multiple GitHub Accounts with Different SSH Keys
description: Streamline your workflow with distinct SSH configurations
date: 2025-05-03
tags: [git, github, ssh]
categories:
- Version Control
---
<p style="color: #5B9BD5; font-style: italic;">
  Note: If you’re new to SSH, please check out my latest post 
  <a href="../ssh-key-beginner-guide" style="color: #6A5ACD; font-style: italic;">
    Complete SSH Key Beginner’s Guide
  </a>, which is more beginner-friendly and comprehensive. This article has more detailed information for those interested in specifics.
</p>

If you're working with multiple GitHub accounts, you might want to keep your credentials separate for each account. This tutorial will show you how to use different SSH keys for two GitHub accounts (`account1` and `account2`) on the same machine.

## 🛠️ Step 1: Generate SSH Keys for Both Accounts

First, generate SSH keys for each account. If you already have one key for `account1`, you'll generate a separate key for `account2`.

**Generate Key for Account 1:**（If you haven’t done so already）
For `account1`, generate an SSH key:

```bash
ssh-keygen -t ed25519 -C "your_email2@example.com" -f ~/.ssh/id_ed25519_account1
```
Note:  
- `ssh-keygen` is used to generate an SSH key pair.
- `-t ed25519`: Uses the `ed25519` algorithm, which is faster and more secure than `rsa`.
- `-C "your_email1@example.com"`: Adds a comment (e.g. your email) for identification purposes.
- `-f ~/.ssh/id_rsa_account1`: Specifies the file where the private key will be saved.

**Generate Key for Account 2:**  
Similarly, generate a separate SSH key for `account2`:

```bash
ssh-keygen -t ed25519 -C "your_email2@example.com" -f ~/.ssh/id_ed25519_account1
```

After creating these keys, make sure to add their corresponding public keys (id_rsa_account1.pub and id_rsa_account2.pub) to the respective GitHub account's SSH settings.

**Add to GitHub**  
After generating the keys, open each public key file (`id_ed25519_account1.pub` and `id_ed25519_account2.pub`) in a text editor, **copy the full contents**, and **paste** it into the corresponding GitHub account’s **SSH keys settings** under:

> GitHub → Settings → SSH and GPG Keys → New SSH key

## ⚙️ Step 2: Configure SSH config File
Next, we’ll configure the SSH settings to ensure that each account uses the correct key.

Open your terminal and edit the SSH config file:

```bash
nano ~/.ssh/config
```

Add the following configuration:

```
# Account 1 - Default GitHub account
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_account1
  IdentitiesOnly yes

# Account 2 - Second GitHub account
Host github-account2
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_account2
  IdentitiesOnly yes
```

Here:

`github.com` is for `account1` (default GitHub account).

`github-account2` is a custom alias for `account2`. This ensures the right SSH key is used.

## 🧑‍💻 Step 3: Clone Repositories Using the Correct Account
When cloning a repository, make sure you use the correct alias for the second account.


```bash
# Clone with Account 1 (default):
git clone git@github.com:account1/repo-name.git
```
```bash
# Clone with Account 2:
git clone git@github-account2:account2/repo-name.git
```
Note: Use `github-account2` as the host to ensure that `account2`'s SSH key (`id_rsa_account2`) is used.

## 📝 Step 4: Set Git Configuration for Each Repository (Optional)
To make sure you’re committing with the correct user for each project, set the `user.name` and `user.email` for each repo.

For Account 1:
```bash
git config user.name "account1"
git config user.email "your_email1@example.com"
```
For Account 2:
```bash
git config user.name "account2"
git config user.email "your_email2@example.com"
```
## ✅ Step 5: Test Which SSH Key Is in Use (Optional)
To check which SSH key is being used:

For Acount 1:

```bash
ssh -T git@github.com
# You should see:
# Hi account1! You've successfully authenticated...
```

For Acount 2:

```bash
ssh -T git@github-account2
# You should see:
# Hi account2! You've successfully authenticated...
```

This confirms the correct SSH key is in use.

## 🌟 Conclusion
You now have separate SSH keys configured for two GitHub accounts. By using different aliases in the SSH configuration, you can easily manage multiple GitHub accounts on the same machine. Always remember to use the correct SSH alias when cloning repositories and pushing changes!
