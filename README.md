# Build a custom video scrubber with Cloudinary and Nuxt.js

![](screenshots/final.gif)

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

Now it's time to add Cloudinary to the mix. You can find the [full install guide here](https://cloudinary.nuxtjs.org/setup).

You may need to install some additional dependencies to get everything workgin.

```
yarn add  @babel/runtime-corejs2
yarn add @soda/get-current-script
```

In your `nuxt.config.js`, be sure to include `useComponent: true` in addition to your Cloudinary credentials. This will tell Nuxt.js to include components from the [Cloudinary Vue SDK](https://cloudinary.com/documentation/vue_video_manipulation). 

```js
export default {
  // ...
  // Modules: https://go.nuxtjs.dev/config-modules
  modules: [
    '@nuxtjs/cloudinary'
  ],
  cloudinary: {
    cloudName: 'demo',
    apiKey: 'demo',
    apiSecret: 'demo',
    useComponent: true
  }
  //...
}
```

## Create the custom Cloudinary Video component

![](screenshots/hello-world.gif)

Then, make a new component for your video player. This is where you'll build the custom video scrubber.

`components/CloudinaryVideo.vue`
```html
<template>
  <div>
    <h1>Hello, world!</h1>

    <cld-video 
      cloudName="demo" 
      publicId="dog" 
      controls="true">
    </cld-video>

  </div>
</template>
```

The `<cld-video>` component is [a video player provided by the Cloudinary Vue SDK](https://cloudinary.com/documentation/vue_video_manipulation#cldvideo_component). With it, you can perform dynamic video transformations right in Vue! To keep things simple, this tutorial will treat it as a simple video player.

## Keeping track of the video time

![](screenshots/current-time.gif)

In order to show the proper scrub position, we need to know the current video time. This time is updated multiple times per second as a video plays.

In order to get the current video in Vue, create a reference to the dom element with `$ref`. In the `<video>` component, add `ref="video"`. Then, the DOM element can be accessed in Vue via `this.$refs.video.$videoElement`.

This `<video>` element has [a method called `onTimeUpdate`](https://www.w3schools.com/jsref/event_ontimeupdate.asp) you can use to get notified of a time change. Then, store that time as a `data` variable.

1. Create a `data` variable called `currentTime`
1. Bind to the `<video>` `onTimeUpdate` event
1. Update data `current` time with the value from the event
1. Render the `currentTime` in the dom

You can see everything come together below:

`components/CloudinaryVideo.vue`
```html
<template>
  <div>
    <h1>Current Time: {{ currentTime }}</h1>

    <cld-video
      cloudName="demo"
      publicId="dog"
      controls="true"
      ref="video"
    ></cld-video>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentTime: 0,
      duration: 0,
    };
  },
  methods: {
    onTimeUpdate(event) {
      this.currentTime = 
        this.$refs.video.$videoElement.currentTime;
    },
  },
  mounted: function () {
    this.$refs.video.$videoElement.addEventListener(
      "timeupdate", this.onTimeUpdate
    );
  },
};
</script>
```

## Controlling Video Time

So how will the video be controlled? Start manipulating the `<video>` time by creating a simple `<button>`.

![](screenshots/go-to-5-seconds.gif)

## Creating the slider

![](screenshots/slider.gif)

## Problems Arise

- glitch outlined here: https://github.com/vuejs/vue/issues/10542#issuecomment-533642739

![](screenshots/glitch.gif)

## Store the currentTime twice to avoid glitches

- don't bind the model because we'll be setting / getting time to much and cause glitch
- fix for glitch is here: https://jsfiddle.net/x1bkLg74/

![](screenshots/glitch-fix.gif)

## Two way binding!

Make background dark.

Styles from here:
- copy slider code from here https://codepen.io/shashank_coder/pen/jOqxOpK

![](screenshots/binding.gif)
