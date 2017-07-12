---
layout: posts
comments: true
published: true
title: Developing for GitHub Pages
categories:
  - development
tags:
  - github-pages
  - docker
---
That's it ! You have decided to create your own site using [*GitHub Pages*][1]. You have followed the GitHub tutorial and you have created your repository with or without a template. What's next ?

To be able to see your local modifications without having to commit and push to GitHub. You will have to [set up a local Jekyll server with the *GitHub Pages* layer][2]. Because it can be annoying, I decided to create a [docker image][4] to simplify this process.

The only thing you have to do is to start a docker container. You can use this
one-liner in your site source directory.

```sh
docker run --name $(basename ${PWD}) \
	--detach --restart unless-stopped \
	--publish 4000:4000 \
	--volume ${PWD}:/var/lib/github-pages \
	jmlemetayer/github-pages
```

Now you can point your browser to <http://localhost:4000> :sunglasses:

## GitHub metadata

The [GitHub Metadata plugin][3], a.k.a `site.github`, is a Jekyll plugin which is part of the *GitHub Pages* layer. It is used to grab informations about the GitHub repository used to generate your site.

If you run the docker container directly into your cloned GitHub repository, this should work. Instead you will have to add the `PAGES_REPO_NWO` environment variable. This variable can also be used to override the repository, if you are using forked repositories by example.

```sh
docker run --name $(basename ${PWD}) \
	--detach --restart unless-stopped \
	--publish 4000:4000 \
	--volume ${PWD}:/var/lib/github-pages \
	--env PAGES_REPO_NWO=username/repo-name \
	jmlemetayer/github-pages
```

Some fields can also request an authentication. This is handled by the `JEKYLL_GITHUB_TOKEN` environment variable and a GitHub generated token.

1. Open <https://github.com/settings/tokens/new>
1. Select the scope `repo > public_repo`, and add a description.
1. Confirm and save the settings. Copy the token you see on the page.
1. Set the `JEKYLL_GITHUB_TOKEN` environment variable with the generated token.

```sh
docker run --name $(basename ${PWD}) \
	--detach --restart unless-stopped \
	--publish 4000:4000 \
	--volume ${PWD}:/var/lib/github-pages \
	--env PAGES_REPO_NWO=username/repo-name \
	--env JEKYLL_GITHUB_TOKEN=123github456token789 \
	jmlemetayer/github-pages
```

## References

1. [GitHub Pages][1]
1. [Setting up your GitHub Pages site locally with Jekyll][2]
1. [GitHub Metadata plugin][3]
1. [Docker Hub: jmlemetayer/github-pages][4]
1. [GitHub project: jmlemetayer/docker-github-pages][5]

[1]: https://pages.github.com
[2]: https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll
[3]: https://github.com/jekyll/github-metadata
[4]: https://hub.docker.com/r/jmlemetayer/github-pages
[5]: https://github.com/jmlemetayer/docker-github-pages