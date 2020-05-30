# 1. Getting Started with React - An Overview and Walkthrough Tutorial
*walkthrough : 연습*<br><br>
written by **Tania Rascia** , **<https://www.taniarascia.com/getting-started-with-react/>**

> I saw what looked like *a bunch of HTML mixed* with JavaScript and thought, isn't this what we've been trying to avoid? *What's the big deal with React?*

### Prerequisites
If you've never used JS or the DOM at all before, see below before trying to tackle React.
  1. Basic familiarity with HTML & CSS
  2. JS
  3. the DOM
  4. ES6 syntax and features
  5. Node.js and npm installed globally
  
### Goals

  1. Learn about essential React concepts! and related terms, such as Babel, Webpack, JSX, components, props, state, and lifecyle **(I think it is very important)**
  2. Build a very simple React app that demonstrates the above concepts.
  
  **Here's the source and a live demo of the end result.**<br>
      <https://github.com/taniarascia/react-tutorial><br>
      <https://taniarascia.github.io/react-tutorial/>
      
 ### WHAT IS REACT?
 
 1. JS library - one of the most popular ones(100,000 stars on Github)
 2. *React is not a framework* (unlike Angular)
 3. React is an open-source project created by **Facebook.**
 4. React is used to build user **interfaces(UI)** on the front end.
 5. React is the **view layer of an MVC application**
 
 One of the most important aspects of React is the fact that you can create **components** (what is a component??), which are like custom, **reusable HTML elements**, to quickly and efficiently build user interfaces. React also streamliness *(간소화하다)* how data is stored and handled, using **state and props** <br>
 
 We'll go over *(거듭 살피다)* all of this and more throughout the article, so let's get started!!
 
 ### Setup and Installation
 
 > There are a few ways to set up React, and I'll show you two so you get a good idea of how it works. <br>
 
 #### 1. Static HTML file
 1. not a popular way but it will be familiar and easy to understand if you've ever used a library like jQuery
 2. load in three CDNs in the `head` - React, React DOM, and Babel.
