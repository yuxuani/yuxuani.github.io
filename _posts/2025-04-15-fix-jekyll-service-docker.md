---
layout: post
title: Fixing Jekyll Service Not Accessible Inside Docker Container
date: 2025-04-15
tags: [docker, jekyll, blogging, debugging]
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
The `asset_img` tag is a custom tag from Hexo (since I was importing old posts into the new website). In this post, how to add an image is described, so there are lines like this `{% raw %}{% asset_img image_name.img display_name %}{% endraw %}` within the article. However, Jekyll does not recognize it, since Jekyll uses Liquid syntax which will contradict with `{% raw %} {% ... %} {%endraw%}` form. As a result, the site build failed, and the service never started.

## ✅ Solution
I edited `_posts/2018-05-19-build-website-with-hexo.md` by adding `raw` and `endraw`  in front of the lines where could be problematic:

{% raw %}
```
{% raw %}{% example code %}{% end %}
```
{% endraw %}

(Simply removing the offending lines and replace with syntax compatible with Jekyll would also work but since the article is introducing hexo, I preserve the information to be displayed.)

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
