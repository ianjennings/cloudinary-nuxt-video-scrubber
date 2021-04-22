<template>
  <div>
    <p>Current Time: {{ currentTime }}</p>
    <p>Duration: {{ duration }}</p>
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
    onLoadedMetadata(event) {
      this.duration = this.$refs.video.$videoElement.duration;
    },
    setVideoTime(timestamp) {
      this.$refs.video.$videoElement.currentTime = timestamp;
    },
  },
  mounted: function () {
    this.$refs.video.$videoElement.addEventListener(
      "timeupdate",
      this.onTimeUpdate
    );

    this.$refs.video.$videoElement.addEventListener(
      "loadedmetadata",
      this.onLoadedMetadata
    );
  },
};
</script>
