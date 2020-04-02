<template>
  <div>
    <!-- <div>
      <el-button @click="open_camera">打开摄像头</el-button>
    </div> -->
    <div class="wrapper">
      <video
        class="video"
        :class="activeDevice === 0 ? 'front' : ''"
        ref="video"
      />
      <!-- <canvas
      style="display:none"
      ref="canva"
    /> -->

      <button
        v-if="videoDevices.length > 1"
        class="button is-rounded is-outlined switch-button"
        @click="switchCamera"
      >
        <b-icon
          pack="fas"
          icon="sync-alt"
        />
      </button>

      <div class="photo-button-container">
        <el-button
          class="button photo-button"
          @click="TakePhoto"
          icon="el-icon-camera-solid"
          circle
        >
        </el-button>
      </div>
    </div>
  </div>
</template>

<script>
// import PhotosGallery from './PhotosGallery.vue';

export default {
  components: {
    // PhotosGallery,
  },
  props: {
    show_mask: Boolean,
  },
  data() {
    return {
      photos: [],
      mediaStream: this.mediaStream,
      videoDevices: [],
      activeDevice: 0,
      counter: 0,
    };
  },
  methods: {
    async StartRecording(deviceIdx) {
      const { video } = this.$refs;
      this.mediaStream = await navigator.mediaDevices.getUserMedia({
        video: { deviceId: { exact: this.videoDevices[deviceIdx].deviceId } },
      });
      video.srcObject = this.mediaStream;
      video.play();
    },
    async TakePhoto() {
      const { video } = this.$refs;
      const { canva } = this.$refs;
      const width = video.videoWidth;
      const height = video.videoHeight;
      canva.width = width;
      canva.height = height;
      const ctx = canva.getContext('2d');
      ctx.save();
      if (this.activeDevice === 0) {
        ctx.scale(-1, 1);
        ctx.drawImage(video, width * -1, 0, width, height);
      } else {
        ctx.drawImage(video, 0, 0);
      }
      ctx.restore();
      this.photos.push({
        id: this.counter + 1,
        src: canva.toDataURL('image/png'),
      });
    },
    switchCamera() {
      const tracks = this.mediaStream.getVideoTracks();
      tracks.forEach((track) => {
        track.stop();
      });
      this.StartRecording((this.activeDevice + 1) % 2);
      this.activeDevice = (this.activeDevice + 1) % 2;
    },
  },
  async mounted() {
    const devices = await navigator.mediaDevices.enumerateDevices();
    this.videoDevices = devices.filter((d) => d.kind === 'videoinput');
    this.StartRecording(0);
  },
};
</script>

<style scoped>
.video.front {
  -webkit-transform: scaleX(-1);
  transform: scaleX(-1);
}
.wrapper {
  background-color: rgb(82, 76, 76);
  opacity: 0.8;
  display: grid;
  width: 100%;
  height: 100%;
  /* grid-template-columns: [left] 90vw [bs] 5vw [es] 5vw [right];
  grid-template-rows: [top] 5vh [bs] 5vh [es] 60vh [middle] 10vh [bottom] 20vh [end]; */
  justify-items: center;
  overflow: hidden;
}
.video {
  height: 100%;
  grid-column: left/right;
  grid-row: top / bottom;
  user-select: none;
  max-width: unset;
}
.switch-button {
  grid-column: bs / es;
  grid-row: bs / es;
  z-index: 5;
  border-radius: 100%;
  width: 6vh;
  height: 6vh;
  font-size: 2vh;
}
.photo-button-container {
  /* grid-column: left / right;
  grid-row: middle / bottom;
  z-index: 5;
  width: 100vw;
  height: 20vh;
  display: flex;
  justify-content: center; */
}
.photo-button {
  /* width: 10vh;
  height: 10vh;
  border-radius: 100%; */
}
.photo-button {
  /* font-size: 4vh;
  color: black; */
}
.gallery {
  grid-column: left / right;
  grid-row: bottom / end;
}
</style>
