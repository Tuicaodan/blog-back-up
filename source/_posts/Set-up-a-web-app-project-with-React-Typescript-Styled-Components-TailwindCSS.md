---
title: >-
  Set up a web app project with React + Typescript + Styled Components +
  TailwindCSS
comments: true
date: 2021-11-18 22:54:24
tags:
categories:
description:
password:
---
This is a short tutorial post as a reminder to myself about how to set up a web app project using the combination of  React + Typescript + Styled Components + TailwindCSS.
<!--more-->
### How to set up

1. cd to the folder where you want to have your react app locate
2. create the react app
    
    ```bash
    npx create-react-app the-app-name --template typescript
    cd the-app-name
    ```
    
3. if you already have a non-Typescript app created, you could add Typescript to the existing project
    
    ```bash
    npm install --save typescript @types/node @types/react @types/react-dom @types/jest
    ```
    
4. install TailwindCSS
    
    ```bash
    #in the root
    npm install -D tailwindcss@npm:@tailwindcss/postcss7-compat postcss@^7 autoprefixer@^9
    ```
    
5. install CRACO
    
    ```bash
    #in the root
    npm install @craco/craco
    ```
    
6.  install and configure CRACO
    1. update your `scripts` in your `package.json` file to use `craco` instead of `react-scripts` for all scripts except `eject`:
        
        ```jsx
        {
          // ...
           "start": "craco start",
           "build": "craco build",
           "test": "craco test",
           "eject": "react-scripts eject"
          },
        }
        ```
        
    2. create a `craco.config.js` at the root of our project and add the `tailwindcss` and `autoprefixer` as PostCSS plugins:
        
        ```jsx
        // craco.config.js
        module.exports = {
          style: {
            postcss: {
              plugins: [
                require('tailwindcss'),
                require('autoprefixer'),
              ],
            },
          },
        }
        ```
        
7. create TailwindCSS configuration file (This will create a minimal `tailwind.config.js` file at the root)
    
    ```bash
    npx tailwindcss-cli@latest init
    ```
    
8. configure `tailwind.config.js` file
    
    ```jsx
    // tailwind.config.js
      module.exports = {
        purge: ['./src/**/*.{js,jsx,ts,tsx}', './public/index.html'],
        darkMode: false, // or 'media' or 'class'
        theme: {
          extend: {},
          //I normally add these screen sizes here for media queries
          screens: {
          sm: "640px",
          md: "768px",
          lg: "1024px",
          xl: "1280px",
          "2xl": "1536px",
      },
        },
        variants: {
          extend: {},
        },
        plugins: [],
      }
    ```
    
9. include Tailwind in the index CSS
    
    ```css
    /* ./src/index.css */
    @tailwind base;
    @tailwind components;
    @tailwind utilities;
    ```
    
10. install twin.marco
    
    ```bash
    npm i twin.marco
    ```
    
11. install Styled Components
    
    ```bash
    npm install --save styled-components
    npm i --save-dev @types/styled-components
    ```
    
12. All done. Ready to go

### Why did I choose these skill stacks

#### Styled Components + TailwindCSS

> ##### What is Styled Components
> styled-components is the result of wondering how we could enhance CSS for styling React component systems. By focusing on a single use case we managed to optimize the experience for developers as well as the output for end users.

> ##### What is TailwindCSS
> Tailwind CSS is a highly customizable, low-level CSS framework that gives you all of the building blocks you need to build bespoke designs without any annoying opinionated styles you have to fight to override.

##### The story

When I first started doing web app development with HTML, CSS, and vanilla JavaScript.  I found one thing that is quite brother me was after creating several HTML elements. Even with the appropriate class/id name for the elements, I always have some messy CSS code. To make the code more maintainable, I have to do refactoring for the CSS. The separated HTML and CSS files made a lot of back and forward movements. 

When I started to learn React, I had the same feeling that it is not easy to make the JSX and CSS clean while coding. After doing some research, I found Styled Components. Using React is similar to playing with Lego bricks. With the help of Styled Components, you can style the Lego bricks during the creation of that brick. The idea is to have the styling and the creating together. Because of this, when you want to change the component styling later, instead of checking the className and chasing it in the CSS file, you can find the component directly and change the styling where the component is.

Furthermore, with the TailwindCSS, creating the styling or changing the styling is much easier. Because TailwindCSs is a low-level CSS framework, it is self-described and highly customizable. 

#### Typescript

I believe once you try Typescript, you will never get back to JavaScript. I have some really bad memories of web development using JavaScript.  One typo in the props attribute might cause hours of debugging. 

Three things I really like the Typescript:

1. Type/interfaces annotations. You can add types to variables or define interfaces for props. So you will get code suggestions while you type. This saves a lot of time and reduces the possibility of having typos/mistakes.
2. Compiling error check. Because Typescript is a statically typed script, so it could show errors before running the code.
3. Good maintainability. Not only for myself. I believe for a new developer to read the code, he/she will really appreciate you using Typescript over JavaScript.

### Pseudocode example

If I want to create a div:

- has a certain styling:
    - has flex display
    - width is 3/4 of its parent in medium to big screen
    - width is 100% of its parent in small screen
    - background-color is grey
    - has auto margin
    - has some padding on the top

- accept props with certain attributes

#### React + Typescript + Styled Components + TailwindCSS

```jsx
import React from 'react';
import syled from 'styled-components';
import tw from 'twin.marco';

interface ArticleProps {
  title: string,
  author: string,
  hasDeleted: boolean,
}

const ArticleWarpper = styled.div`
  ${tw`
    w-3/4
    sm:w-full
    flex
    flex-row
    bg-gray-400
    m-auto
    pt-2
  `}
`
const WordWarpper = styled.div`
  ${tw`
    item-center
    px-2
  `}
`

const Article: React。FC<ArticleProps> = props => {
  return (
    <ArticleWarpper>
      {props.hasDeleted && (
        <WordWarpper> The article has been deleted </WordWarpper> 
      )}
      {!props.hasDeleted && (
        <WordWarpper> Title: {props.title} </WordWarpper> 
        <WordWarpper> Author: {props.author} </WordWarpper> 
      )}
    </ArticleWarpper>
  )
}
export default Article;
```

#### React alone

```jsx
import React from 'react';
import './Article.css';

const Article = props => {
  return (
    <div className="ArticleWarpper">
      {props.hasDeleted && (
        <div className="WordWarpper"> The article has been deleted </div> 
      )}
      {!props.hasDeleted && (
        <div className="WordWarpper"> Title: {props.title} </div> 
        <div className="WordWarpper"> Author: {props.author} </div> 
      )}
    </div>
  )
}
export default Article;
```

Then I have to write the CSS in a separate CSS file.

There are several things I like using the mentioned tech stacks:

- If I need to change any style of the component, I can have this done in one place
- Keep in mind that the CSS globaly used. If using the plain React, change ths css could affects all the components contain the same `className`
- The TailwindCSS make the style easy to write and easy to read (I really like the way TailwindCSS come up with to write the media queries)
- The `ArticleProps` interface provides the auto-fill ability for the props. Improve effectiveness.
- With the help of The `ArticleProps` interface, the code will check the attributes when you provide props in the parent component
- Another benefit of the interface is comprehensibility. No matter reading other people's code or reading the code you wrote a couple of years before, the interface could help you understand the code better