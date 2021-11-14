---
title: How to set up NexT theme in Hexo
comments: true
date: 2021-11-14 22:58:09
tags: [Hexo, blog, NexT]
categories: Hexo
description:
---
The Hexo came with a default theme which is okay. You can design your own theme or use other users' designs if you want to make it easy. Currently, there are more than 300+ themes posted [here]([https://hexo.io/themes/](https://hexo.io/themes/)). I found some of the themes were stopped to update by the authors a couple of years ago. One of the parameters when I picked the theme, one of the parameters is that the last update should be within a year ago. So there might be less possibility of compatible issues with the newer versions of Hexo. 

<!--more-->

I decided to go with the NexT theme since it really aligns with my minimalism guideline. Here is the [repo]([https://github.com/theme-next/hexo-theme-next](https://github.com/theme-next/hexo-theme-next)). 

## How to install NexT

1. In the Hexo root folder, install through npm
    
    ```bash
    $ npm install hexo-theme-next
    ```
    
2. Or you can clone the repo instead of npm installation
    
    ```bash
    $ git clone https://github.com/next-theme/hexo-theme-next themes/next
    ```
    
3. changes the `theme` setting in the `_config.yml`  file in the Hexo root folder:
    
    ```yaml
    theme: next
    ```
    
4. Now you have installed the NexT theme

## Bits and bobs about how I set up

- There are hundreds of different settings in the NexT theme. I just list some of the features/settings I found were quite useful/interesting.
- There are two different `_config.yml`:
    - One is Hexo settings, located at:
        
        ```
        /hexo/_config.yml
        ```
        
    - One is NexT theme settings, located at:
        
        ```
        /hexo/themes/net/_config.yml
        ```
        

### 1. Add about/tags/categories pages

- In the theme settings yml
    
    ```yaml
    menu:
      home: / || fa fa-home
      about: /about/ || fa fa-user
      tags: /tags/ || fa fa-tags
      categories: /categories/ || fa fa-th
      #archives: /archives/ || fa fa-archive
      #schedule: /schedule/ || fa fa-calendar
      #sitemap: /sitemap.xml || fa fa-sitemap
      #commonweal: /404/ || fa fa-heartbeat
    ```
    

### 2. change between different NexT themes

- NexT has four different themes. You could switch between them without changing another else(sweet!)
- In the theme settings yml
    
    ```yaml
    # Schemes
    #scheme: Muse
    scheme: Mist
    #scheme: Pisces
    #scheme: Gemini
    ```
    

### 3. Display current reading percentage

- In the theme settings yml
    
    ```yaml
    # Scroll percent label in b2t button.
      scrollpercent: true
    ```
    

### 4. Add searching feature

- Need to install a third-party plugin
    
    ```yaml
    npm install hexo-generator-searchdb --save
    ```
    
- in the Hexo settings yml
    
    ```yaml
    # Add local searching function
    search:
      path: search.xml
      field: post
      format: html
      limit: 100
    ```
    

### 5. Change site icons

- Prepare an icon file(ideally 32*32) and change the file name to `favicon.ico`.
- Locate the icon file to `/themes/next/source/images`
- Change the theme settings yml
    
    ```yaml
    favicon:
      small: /images/favicon.png
      medium: /images/favicon.png
      apple_touch_icon: /images/favicon.png
      safari_pinned_tab: /images/favicon.png
    ```
    

### 6. Add password feature
- Need to install a third-party plugin
    
    ```yaml
    npm install hexo-hexo-blog-encrypt --save
    ```
    
- When writing new articles, add these to the head
    
    ```markdown
    ---
    title: Hello World
    tags: [test, password]
    password:123456
    ---
    ```
    

### 7. Add word count and estimate reading time

- Need to install a third-party plugin
    
    ```yaml
    npm install hexo-wordcount --save
    ```
    
- Add this to the Hexo settings yml
    
    ```yaml
    # Symbols count and time to read for articles in Hexo blog.
    symbols_count_time:
      symbols: true
      time: true
      total_symbols: true
      total_time: true
      exclude_codeblock: false
      awl: 4
      wpm: 275
      suffix: "mins."
    ```
    

### These are the features I implemented for this blog. I will update this list once I make other changes to the blog.