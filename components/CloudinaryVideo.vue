<template>
  <div>
    <p>Current Time: {{ currentTime_ }}</p>
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

    <div>
      <input
        type="range"
        :min="0"
        :max="duration"
        v-model="currentTime"
        class="slider"
        id="myRange"
      />
    </div>
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
      currentTime_: 0,
      duration: 0,
    };
  },
  methods: {
    showList() {
      this.show = true;
    },
    onTimeUpdate(event) {
      this.currentTime_ = this.$refs.video.$videoElement.currentTime;
    },
    onLoadedMetadata(event) {
      this.duration = this.$refs.video.$videoElement.duration;
    },
    setVideoTime(timestamp) {
      this.$refs.video.$videoElement.currentTime = timestamp;
    },
  },
  computed: {
    currentTime: {
      get: ({ currentTime_ }) => currentTime_,
      set(time) {
        this.setVideoTime(time);
      },
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
