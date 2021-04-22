<template>
  <div>
    <h3>Current Time: {{ currentTime }}</h3>
    <div>
      <button v-on:click="setVideoTime(5)">Go to 0:05</button>
    </div>

    <cld-video
      cloudName="demo"
      publicId="dog"
      controls="true"
      ref="video"
    ></cld-video>
  </div>
</template>

<style scoped>
video {
  width: 400px;
}
</style>

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
    setVideoTime(timestamp) {
      this.$refs.video.$videoElement.currentTime = timestamp;
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
