---
title: Setting up my Digital Garden
draft: false
tags:
  - DigitalGarden
---
## Choosing the platform
When searching for good methods to organize and publish my projects as a portofolio, there were various options such as
- Notion
- Obsidian
- Personal web page
- Github repo

I liked the graph view and the diverse community plugins of Obsidian, but I was hesitant because of Obsidian Publish's fee and lack of freedom in customizaiton.
Then I came across Quartz, a static-site generator for obsidian vaults. This lead me to choose Obsidian over other options.

## Issues
This being my first post, I would like to mention some issues I had while following the instructions from the offical [documentation](https://quartz.jzhao.xyz/).

### Repository Visibility
When creating a new repository, you can to set the visibility to either private or public. However if you are planning to host your garden through Github Pages without Github Pro plan, you must set it as a *public* repo.

### Setting up your Github Repository
When setting up the Github repository, there's a step where you add REMOTE-URL and adding upstream for quartz updates. I faced an issue regarding this code block, saying the remote origin was already set.

This was resolved by simply *changing* the remote url to your repository's url, and leaving the upstream since it was already set due to cloning.

```
git remote set-url origin your-git-url.git
```

