---
layout: post
title: Build up Your Own Website with Hexo
description: Get started with hexo
date: 2018-05-19 15:44:43
language: en
tags:
- hexo
- blogging
categories:
- Web
---
How to get started with Hexo?
## Install Git and Node.js
First, install [Git][2] and [Node.js][3]. You can check if they are successfully installed by tying the following commands.

```bash
git version
node -v
```
## Install Hexo
Type in the following command:

```bash
npm install hexo-cli -g
```
For version checking, you may type in

```bash
hexo -v
```
## Create your website
- Type in `hexo init website_name` and Hexo will generate a template for you.
- `cd` to the folder you just created
- run `hexo server` and you can see the site in the localhost.

```bash
hexo init website_name
cd website_name
hexo server # alternatively hexo s
```

## Customize your website
Some basics:
### Configuration

- Go to the folder and configurate the `_config.yml` file.
- In the `source` folder, there is a folder called `_posts`. That is where you can put your posts.


```bash
hexo new post_name # create a new post
hexo new draft draft_name # create a draft
hexo server --draft # show the draft
hexo publish draft_name # post the draft
hexo new page page_name # create a new page
```

### Modification of Front Matter
Your can modify your page or posts by just modifying the **front matter**. (see [Hexodocs: Front Matter][4]. ) Here is an example of sorting your posts by adding tags and categories.

```yaml
---
title: Post's title
date: 2018-05-19 13:54:51
tags: [Tag1, Tag2, Tag3]
categories:
- [Cat1, Cat1.1]
- [Cat2]
- [Cat3]
---
```

**Now you're running your website, but you can do more to make your site to look like exactly what you want.**

## Furthermore
More things you can do with hexo:

### Change the theme
With Hexo, you are able to change the theme without changing your content files. To change it, you may
- go to the [official site][5] and select a theme
- go to git, read the `README` file and see the features to decide whether to take it
- clone it from the git `git clone https://... themes/theme_name`
- change the theme in the `_config.yml` file
- restart your host and you can see the new theme

### Asset-folders
An asset-folder is a folder to store the file that you want to display or let the reader downloading. You can

- go to `_config.yml` file
- set `post_asset_folder: true` and save
- when you create a new post, an `assetfolder` will be generated at the same time
- put the file into the folder
- write the code in the content

Example: adding an image
{% raw %}
```
{% asset_img image_name.img display_name %}
{% asset_link image_name %}
{% asset_path image_name %}
```
{% endraw %}

### Plugins
See https://hexo.io/plugins/

Examples:
- add codeblock

{% raw %}
```
{% codeblock lang=python %}
print('Hello World')
{% endcodeblock %}
```
{% endraw %}

- add youtube video

{% raw %}
```
{% youtube YouTubeID=xxxxxx %}
```
{% endraw %}

**Actually you can do a lot more with Hexo. You may want to characterize your website or even create your own theme. To go deeper, reading the [documentation][1] on the official website is neccessary. Plus, to get started, there is a series of [tutorial videos][6] provided by Mike from [Giraffe Academy][7], which is very helpful. Hope that you can enjoy it!**

## References
[Hexodocs][1]
[Hexo Tutorial by Mike][6]

[1]: https://hexo.io/docs/index.html
[2]: https://git-scm.com/
[3]: https://nodejs.org/en/
[4]: https://hexo.io/docs/front-matter.html
[5]: https://hexo.io/themes/index.html
[6]: https://www.youtube.com/watch?v=Kt7u5kr_P5o&list=PLLAZ4kZ9dFpOMJR6D25ishrSedvsguVSm&index=1
[7]: http://www.giraffeacademy.com/
