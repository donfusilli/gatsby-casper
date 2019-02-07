---
layout: post
title: How to Make a Circular Image
image: img/code-3.jpg
author: Don
date: 2019-02-06T07:03:47.149Z
draft: false
tags: []
---

You'll often see a circular image used for profile avatars, like the one at the bottom
of this page. In the past, this was a bit of a pain to get rendering correctly across
all browsers and devices. Nowadays, this can be easily accomplished with the 
<a href="https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius" target="_blank">border-radius</a>
CSS property.

For good measure, let's ensure the image is a square - the width and height should be equal. If your image
isn't a square, you can crop the image so that it becomes a square. If you're not sure which program to use
in order to crop your image, I would recommend trying <a href="https://www.gimp.org/" target="_blank">GIMP</a>.

Suppose we have the following image, 200px width by 200px height:


![Profile Image](img/profile.jpeg)


With the following, we can make the square image into a circular image!

```css
border-radius: 50%;
```

![Profile Image Circular](img/profile-circular.png)