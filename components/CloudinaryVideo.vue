<template>
  <div>
    <cld-video cloudName="demo" publicId="dog" controls="false" ref="video">
      <cld-transformation width="0.4" angle="20" />
      <cld-transformation
        overlay="cloudinary_icon_white"
        width="60"
        opacity="50"
        gravity="south_east"
        y="15"
        x="60"
    /></cld-video>

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
      // return the actual video time instead of virtual time
      get: ({ currentTime_ }) => currentTime_,
      // virtual time updates actual video time
      set(time) {
        this.setVideoTime(time);
      },
    },
  },
  mounted: function () {
    console.log(this.$refs.video);

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
