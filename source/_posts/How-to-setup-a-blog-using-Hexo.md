---
title: How to setup a blog using Hexo
comments: true
date: 2021-11-09 22:29:46
tags: [Hexo,blog]
categories: Hexo
description:
---
### The story

I keep listening about how important a developer should have a tech blog. A tech blog could both benefit other people and me. After wasting a couple of months to do so, I finally take my step. 

<!--more-->

### Why did I choose Hexo

I chose Hexo + GitHub for my blog. The most important reason is that I want to have full control of the blog while not paying too much attention to the server/domain/etc. The Hexo + GitHub combination gives me lots of flexibility on the styling, theme, third-party plugin or so. Here are some advantages I believe is quite important

- Hexo generates a static webpage which means the speed it fast
- Hexo uses Markdown for posting
- The deployment is really straightforward.
- If you want, you could make the blog really complex(need to understand some source code)
- All the files stored on GitHub(free and safer than other free hosts?)

### What is Hexo

Here is the quote from Hexo website:

> Hexo is a fast, simple and powerful blog framework. You write posts in [Markdown](http://daringfireball.net/projects/markdown/) (or other markup languages) and Hexo generates static files with a beautiful theme in seconds.

### Install Hexo

1. Before installing Hexo, you should have Git, Node.js, npm installed.
2. Here is the command from the office doc:
    
    ```bash
    npm install -g hexo-cli
    ```
    
3. After install, use this command to check whether the Hexo is installed correctly
    
    ```bash
    hexo -v
    ```
    
4. initiate Hexo:
    
    ```bash
    hexo init blog-folder-name
    
    cd blog-foler-name
    npm install
    ```
    
5. static file generation and run server
    
    ```bash
    hexo g
    hexo s
    ```
    
6. Then you should be able to see your Hexo blog on the `localhost:4000`

#### The problem

- I had some issues with Hexo installation. After installation, the `hexo -v` command will return this error: `command not found: hexo`.
- A little background story: I changed the location of npm global packages since I want to avoid using `sudo` for npm packages installation.
- So I believe the problem that I cannot run `hexo` command is because of the changes in the environment variables.

#### The solution

1. After several hours of searching, I realized the easiest way is to install and use Hexo locally.
2. I create a folder, run `npm init` in the folder and then install hexo `npm install hexo-cli` 
3. use `npx hexo -v` to check whether I have hexo installed. 
4. initiate Hexo and rest are the same as above. Besides, you have to use `npx` to run hexo locally :
    
    ```bash
    npx hexo init hexo-blog
    ```
    
5. cd to the hexo-blog folder and do dependencies installation
    
    ```bash
    cd hexo-blog
    npm install
    ```
    
6. The generate and run commands are:
    
    ```bash
    npx hexo g
    npx hexo s
    ```
    

### Create a GitHub repository for the blog

1. Create a new repository, make sure it is public
    
    ![create a new repository](https://i.imgur.com/ZAOvxhq.png)
    
2. Check the repository>Settings>Pages>Source is correct
    
    ![pages setting](https://i.imgur.com/ngN3TfF.png)
    

### Deploy Hexo blog to GitHub

1. Go to the blog folder, open the site setting file `_config.yml` and change the `deploy` section to your GitHub repository address:
    
    ```yaml
    deploy:
      type: git
      repository: https://github.com/[Your-GitHub-Username]/[repo-name]
      branch: main
    ```
    
2. Install hexo deployer
    
    ```bash
    npm install hexo-deployer-git
    ```
    
3. clean the bin, generate, and then deploy
    
    ```bash
    npx hexo clean
    npx hexo g
    npx hexo d
    ```
    
4. Now you should be able to see the default Hexo blog using the URL provided in the GitHub Pages.