# cloudinary-vue-nuxt

```sh
ianjennings@Gibson:~/Development-Unix$ npm init nuxt-app cloudinary-vue-nuxt

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
