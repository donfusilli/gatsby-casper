---
layout: post
title: Improve Component Development with Storybook
image: img/storybook.png
author: Don
date: 2019-02-09T07:03:47.149Z
draft: false
tags: ["storybook"]
---

Especially with the rise in popularity of React, web development in general is moving toward a
more component-based architecture. When developing a site or app, large or small, you'll want to
break down the pages, templates, etc. into separate blocks that can be easily reused. This is what
I mean when I say "component development".

It's helpful to organize your components into a single place where other developers, QA engineers,
and project managers can go to look at them. Even if you're working solo, it's still a good idea
to have an easy way to show off the components to the client, or at the very least, a quick way for you to review all your components.

The idea of a style/component guide is not something new, but Storybook does a great job
formalizing component development, especially when using React, React Native, Angular, and Vue.
It's also quick and easy to set up, without needing to change your components. For full
documentation, see <a href="https://storybook.js.org/basics/quick-start-guide/" target="_blank">https://storybook.js.org/basics/quick-start-guide/</a>. 

---

Let's say we're using React for this example and have the following directory structure:

```
- package.json
- src
    - server
    - client
        - components // <-- our React components live here
            - MyComponent.jsx
            ... // other components
```

Just for this demo, say `MyComponent.jsx` contains the following:

```jsx
class MyComponent extends React.Component {
    render() {
        return <h1>Hello, {this.props.name}</h1>;
    }
}
```

## Install NPM Modules

We're going to need a few npm modules to start.

```js
npm i --save-dev @storybook/react
npm i --save react react-dom
npm i --save-dev @babel/core
npm i --save-dev babel-loader
```

`@storybook/react` is the main npm module to get Storybook working with React (as the name implies). In addition to that, it lists the other 4 modules as peer dependencies, so we'll
have to manually install those as well. See <a href="https://nodejs.org/en/blog/npm/peer-dependencies/" target="_blank">here</a> for info about peer dependencies.

## Add an npm script to start Storybook

```
// package.json
{
  "scripts": {
    "storybook": "start-storybook -p 9001 -c .storybook"
  }
}
```

The `-p` param denotes port number and `-c` denotes the directory that contains the config
file we'll be adding in the next step. It's convention that this directory is called
`.storybook`, but you're free to change it if you want.

By adding this script to `package.json`, you'll be able to run `npm run storybook` and then
visit `localhost:9001` in your browser to see your stories. But we have to add our config file
and stories first.

## Add a config file

In the config, we need to import the `configure` function from `@storybook/react`, create a
function that requires our stories, and then invoke the `configure` function with the function that requires stories as an argument. Probably easier to look at the code:

```js
// .storybook/config.js
import { configure } from '@storybook/react';

function loadStories() {
  require('./stories/myComponent.js');
  ... // require as many stories as you need
}

configure(loadStories, module);
```

## Let's review the directory structure

Here's what the directory structure will look like after adding the Storybook files/folders we
need for a single story for `MyComponent`:

```
- package.json
- src
    - server
    - client
        - components // <-- our React components live here
            - MyComponent.jsx
            ... // other components
- .storybook
    - config.js
    - stories
        - myComponent.js
```

## Write your stories

```jsx
// .storybook/stories/myComponent.js
import React from 'react';
import { storiesOf } from '@storybook/react';
import MyComponent from '../../src/client/components/MyComponent.jsx';

storiesOf('MyComponent', module)
  .add('with a name', () => (
    <MyComponent name="Don" />
  ))
  .add('with no name', () => (
    <MyComponent />
  ));
```

Each use case for your component is a different story. In the above, we have 2 stories for
the `MyComponent` component: when a `name` prop is passed to it, and when nothing is passed
to it.

We add a story using the `add` function, which accepts a string that describes the use case, and
a function that returns your component with whatever props you want to pass to it.

## Run Storybook in the browser 🥁

Run Storybook with `npm run storybook`, which calls the npm script we added earlier to package.json. That in turn runs `start-storybook -p 9001 -c .storybook`.

Visit `localhost:9001` to see your 2 stories! 🎊

When you edit your components used in the stories, you'll see your changes in the browser
automatically without having to reload the page. This is because Storybook uses Webpack's
hot module reloading.

You can view the different stories by selecting them in the sidebar to the left. Stay tuned for
future posts where I'll share some Storybook add-ons that can be useful.