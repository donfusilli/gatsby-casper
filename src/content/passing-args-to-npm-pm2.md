---
layout: post
title: Passing Arguments to NPM target in PM2 Configuration File
image: img/code-1.jpg
author: Don
date: 2019-01-21T07:03:47.149Z
draft: false
tags: []
---

Today I was wondering how we can pass arguments to an npm run target when using the node process manager PM2:
http://pm2.keymetrics.io/.

In other words, say you have the following command to run: `pkg develop -p 9999`, where 
    
    - `develop` is a script defined in your package.json, which runs `pkg develop`
    
    - `p` represents an argument passed to the script, in this case, the port number

How do you define this command in your PM2 configuration file?

---

## File Structure

Assume the following file structure:

```css
- javascript
    -- package.json
    -- npm-shrinkwrap.json
- pm2
    -- config.json
```

## package.json

```css
{
    name: "my package.json",
    version: "1.0.0",
    description: "",
    main: "index.js",
    scripts: {
        develop: "pkg develop",
    },
    author: "Don",
    dependencies: {
        ...
    },
    devDependencies: {
        ...
    }
}
```

## pm2/config.json

The key is to use PM2's `args` parameter, which accepts an array (list) of strings that comprise
the command you need to run.

See http://pm2.keymetrics.io/docs/usage/application-declaration/ for more info on all the
configuration variables you can use.

Additionally, the double dash between `develop` and `-p` in the `args` array denotes that the
arguments that come after the double dash are meant to be passed to `pkg develop`.

More on the double dash: 
https://stackoverflow.com/questions/26282344/what-does-double-dash-do-when-following-a-command

```css
{
    "name": "my-pm2-process",
    "cwd": "/home/don/project.com",
    "exec_mode": "fork",
    "env": { "NODE_ENV": "development" },
    "script": "npm",
    "args": ["run", "develop", "--", "-p", "9999"],
    ...
}
```
