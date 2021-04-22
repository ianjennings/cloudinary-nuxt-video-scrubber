<template>
  <div>
    <cld-video
      cloudName="demo"
      publicId="dog"
      controls="false"
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
.slider {
  width: 400px;
  height: 15px;
  -webkit-appearance: none;
  background: #111;
  outline: none;
  border-radius: 15px;
  overflow: hidden;
  box-shadow: inset 0 0 5px rgba(0, 0, 0, 1);
}
.slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 15px;
  height: 15px;
  border-radius: 50%;
  background: #0069ff;
  cursor: pointer;
  border: 4px solid #333;
  box-shadow: -407px 0 0 400px #0069ff;
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
