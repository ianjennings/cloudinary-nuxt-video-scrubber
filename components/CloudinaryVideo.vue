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
    showList() {
      this.show = true;
    },
    onTimeUpdate(event) {
      this.currentTime = this.$refs.video.$videoElement.currentTime;
    },
  },
  mounted: function () {
    console.log(this.$refs.video);

    this.$refs.video.$videoElement.addEventListener(
      "timeupdate",
      this.onTimeUpdate
    );
  },
};
</script>
