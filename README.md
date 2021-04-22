# Build a custom video scrubber with Cloudinary and Nuxt.js

Nuxt is a static-site generator that upgrades the modularity of Vue.js for full-fledged web applications. Nuxt helps developers create fast and SEO optimized single page applications. We often see Nuxt powering blogs and other text based sites.

But it doesn't end there! As Nuxt is based on Vue.js, there's no reason to be limited to text. This tutorial will demonstrate how you can extend Nuxt to serve and control video content with the Cloudinary Video player. 

Cloudinary is an API for hosting and transforming image and video content. It's a great choice for a Nuxt project as you're guaranteed fast delivery. It's all about speed here. Cloudinary even has a handful of prebuilt Vue components you can use to modify your videos without a backend! 

## Project Set Up

First, create a new Nuxt app. The `nuxt-app` package is the [recommended](https://nuxtjs.org/docs/2.x/get-started/installation/) way to start a new project. In your console, run the following command:

```sh
yarn create nuxt-app cloudinary-vue-nuxt
```

Then follow the interactive prompts. You can find the options used for this demo below.

```sh
ianjennings@Gibson:~/Development-Unix$ yarn create nuxt-app cloudinary-vue-nuxt

create-nuxt-app v3.6.0
✨  Generating Nuxt.js project in cloudinary-vue-nuxt

? Project name: cloudinary-vue-nuxt
? Programming language: JavaScript
? Package manager: Npm
? UI framework: None
? Nuxt.js modules: (Press <space> to select, <a> to toggle all, <i> to invert selection)
? Linting tools: (Press <space> to select, <a> to toggle all, <i> to invert selection)
? Testing framework: None
? Rendering mode: Universal (SSR / SSG)
? Deployment target: Static (Static/Jamstack hosting)
? Development tools: (Press <space> to select, <a> to toggle all, <i> to invert selection)
? What is your GitHub username? ianjennings
? Version control system: Git
```

Now that you have a clean Nuxt project, you should be able to use the `dev` command to run the project:

```sh
yarn dev
```

This will create a development server on `localhost:3000` where you can preview your changes.

## Install the Cloudinary Nuxt Package

Now it's time to add Cloudinary to the mix. Cloudinary 

find the install guide here:
https://cloudinary.nuxtjs.org/setup

Some needed dependencies:
```
yarn add  @babel/runtime-corejs2
yarn add @soda/get-current-script
```

```
yarn dev
```

- add the modules / setup
- create the new file
- get the video by reference
- [look at commits]
- don't bind the model because we'll be setting / getting time to much and cause glitch
- fix for glitch is here: https://jsfiddle.net/x1bkLg74/
- glitch outlined here: https://github.com/vuejs/vue/issues/10542#issuecomment-533642739
- make dark background
- copy slider code from here https://codepen.io/shashank_coder/pen/jOqxOpK

## Feedback

- great that the demo keys actually work
- some dependency issues

this demo did not rotate the dog
different dog than screenshot
```html
<cld-video cloudName="demo" publicId="dog" controls="true" >
  <cld-transformation width="0.4" angle="20" />
  <cld-transformation overlay="cloudinary_icon_white" width="60" opacity="50" gravity="south_east" y="15" x="60" />
</cld-video>
```

## Build Setup

```bash
# install dependencies
$ npm install

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm run start

# generate static project
$ npm run generate
```

For detailed explanation on how things work, check out [Nuxt.js docs](https://nuxtjs.org).
