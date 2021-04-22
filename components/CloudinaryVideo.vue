<template>
  <div>
    <h1>Hello, world!</h1>

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
      show: false,
    };
  },
  methods: {
    showList() {
      this.show = true;
    },
  },
  mounted: function () {
    console.log(this.$refs.video);
  },
};
</script>
