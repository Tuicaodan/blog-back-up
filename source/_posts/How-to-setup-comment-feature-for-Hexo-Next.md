---
title: How to setup comment feature for Hexo Next
comments: true
date: 2021-11-08 23:00:25
tags: [Hexo, Comment, Blog]
categories: Hexo
description:
---
## Overviews

This is a tutorial for setting up the comment feature for Hexo + Next. There are a couple of options for this feature. I think Disqus is the option for easier implementation. However, the Disqus requires users to have a Disqus account before commenting. Another option is using Valine. The setup was a little bit complex than Disqus. But it will give more control for the comment information.

<!--more-->
____
### 2021-11-09 Updates 
I found the Valine might have some conflicts with either the Next theme or multiple levels of headings in Markdown. When I have two or more levels of headings， after deployment, the Valine comment section will disappear. By checking the console, I found the error is `Uncaught TypeError: Valine is not a constructor`. Couldn't find any similar situation or solution yet. Well, it was fun while it didn't have the bug. So, at least for now, I have to switch to Disqus.

____
## Disqus

- Create a Disqus account. Choose the I want to use "Disqus on my site" option.
- Create the `shortname` you entered.
- You should be able to login to the manager site by using this URL:
  ```
  https://YOUR_SHORTNAME.disqus.com/admin/settings/general
  ```
- Once you have the `shortname`, update the Next theme `_config.yml`
  ```yaml
  disqus:
    enable: true
    shortname: YOUR_SHORTNAME
    count: true
    lazyload: false
  ```
- Done. Now you have the Disqus comment feature for the site
____
## Valine

### The basic

1. In order to implement Valine, you need a LeanCloud account.
2. Go to [LeanCloud](https://console.leancloud.app/login?from=%2Fapps), register, and log in.
3. Create an app(developer)
   ![Leancloud Settings](https://i.imgur.com/wCAS5uq.png)
4. In `Setting > Security` turn off all the options other than `LeanStorage`
   ![Leancloud Security Settings](https://i.imgur.com/2WkEGst.png)
5. Create a new class in the `Data Storage > Date`. Make sure the class has `No restrictions`.
   ![Create a class](https://i.imgur.com/CN2mPf0.png)
6. In the `Setting > App Key`, grab the `App ID` and `App Key`.
7. Update the Next theme `_config.yml`

   ```yaml
   # Valine.
   # You can get your appid and appkey from https://leancloud.cn
   # more info please open https://valine.js.org
   valine:
     enable: true
     appid: xxxxxxxxx # your leancloud application appid
     appkey: xxxxxxxxx # your leancloud application appkey
     notify: true # mail notifier , https://github.com/xCss/Valine/wiki
     verify: true # Verification code
     placeholder: # comment box placeholder
     avatar: # gravatar style
     guest_info: nick,mail,link # custom comment header
     pageSize: 10 # pagination size
   ```

8. Restart the server. Now you have the comment feature in the post
____
### Bits and bobs

#### Remove comment feature from about/tags/categories/etc.

I found that not only the post pages but also the about/tags/categories can have comments. This looks a little weird to me. I found there are two approaches too ban the comment feature in these sections.

1. Approach 1
   - The idea is to find the themes layout file and add conditions to the comment section.
   - For Next theme, the layout file locates at `themes/layout/_layout.sig`
   - Find these lines in the file:
     ```cpp
     {% include '_partials/comments.swig' %}
     ```
   - Change it to:
     ```cpp
     {%- if page.type !== 'about' and page.type !== 'tags' and page.type !== 'categories' %}
         {% include '_partials/comments.swig' %}
     {%- endif %}
     ```
2. Approach 2
   - add the following in the `scaffolds/post.md`
     ```markdown
     ---
     title: { { title } }
     date: { { date } }
     comments: true
     categories:
     tags:
     ---
     ```
   - add the following in the about/tags/categories/etc files.
     ```markdown
     ---
     title: categories
     date: 2018-12-06 22:54:28
     type: "categories"
     comments: false
     ---
     ```
____
#### Change the "Valine" in the post header to "Comment"

By default, the post header looks like this:
![comment title](https://i.imgur.com/WRJzAVX.png)

I think the word "Comment" makes more sense than " Valine". Here is the solution:

- Find the `valine.js` file in `/themes/next/scripts/filters/comment/valine.js`
- Find this line in the file:
  ```cpp
  ${iconText('far fa-comment', 'valine')}
  ```
- Change the line to this:
  ```cpp
  ${iconText('far fa-comment', 'comment')}
  ```
- Restart the server
____
#### Change Valine default language

The default language of Valine is Chinese. If you want to change it to English, here is the simple solution:

- Find the file `/themes/next/layout/_third-party/comments/valine.swig`
- Change the `lang` to:
  ```cpp
  lang       : '{{ theme.valine.language }}',
  ```
____
#### Change the default Avatar

Update the Next theme `_config.yml`:

```yaml
valine:
  enable: ture
  appid: xxxxxx-xxxxx # Your leancloud application appid
  appkey: xxxxxxxxxxx # Your leancloud application appkey
  notify: false # Mail notifier
  verify: true # Verification code
  placeholder: Just go go # Comment box placeholder
  avatar: mp # (''/mp/identicon/monsterid/wavatar/robohash/retro/hide)
```