---
layout: post
title: Fixing Jekyll Service Not Accessible Inside Docker Container
date: 2025-04-15
tags: [Docker, Jekyll, Blogging, Debugging]
---

While setting up a blog using the `amirpourmand/al-folio` Jekyll Docker image, I ran into an issue where the local site running inside the container was no longer accessible. Here's a breakdown of how I diagnosed and resolved the problem.

---

## 🧩 Problem

I ran the container with the following command:

```bash
docker run -p 8080:8080 amirpourmand/al-folio:v0.14.4
```

Accessing http://localhost:8080 in the browser resulted in a connection failure. The container was running properly and ports were mapped:

```bash
docker ps
# PORTS: 0.0.0.0:8080->8080/tcp
```

However, inside the container:

```bash
docker exec -it yuxuanigithubio-jekyll-1 /bin/bash
curl http://localhost:8080
# => curl: (7) Failed to connect to localhost port 8080
```
## 🔍 Investigation
Tools like `netstat` and `ss` were unavailable in the container, so I used `curl` to test the local port. `curl` failed to connect, indicating the server wasn't running or listening on the expected port. I exited the container and checked the logs:

```bash
docker logs yuxuanigithubio-jekyll-1
```
The logs showed this error:

```text
Liquid Exception: Liquid syntax error (line 84): Unknown tag 'asset_img'
in /srv/jekyll/_posts/2018-05-19-build-website-with-hexo.md
```

## 🎯 Root Cause
The `asset_img` tag is a custom tag from Hexo (since I was importing old posts into the new website). Jekyll and the al-folio theme do not recognize this tag. As a result, the site build failed, and the service never started.

## ✅ Solution
I edited `_posts/2018-05-19-build-website-with-hexo.md` -- removed the offending line including {% raw %}`{% asset_img ... %}`{% endraw %} and `replaced it with standard Markdown image syntax:`

```markdown
![Alt Text](/assets/images/example.jpg)
```
## 🔁 Restart and Verify
```bash
docker restart yuxuanigithubio-jekyll-1
docker logs yuxuanigithubio-jekyll-1
```
After confirming there were no errors, I accessed `http://localhost:8080`.
Everything worked as expected ✅

## 📝 Conclusion
Sometimes, Jekyll failures are silent within Docker—containers appear to be running, but services are not. Always check the logs, especially if you're migrating posts from platforms like Hexo that use custom syntax.

Hopefully this helps someone facing the same issue 🙌
