<template>
  <div>
    <div class="login-container">
      <h1 class="title">注册</h1>
      <el-form
        label-position="left"
        label-width="20%"
      >
        <el-form-item label="用户名">
          <el-input v-model="username"></el-input>
        </el-form-item>
        <el-form-item label="密码">
          <el-input
            @keydown.native.enter="register"
            show-password
            v-model="password"
          ></el-input>
        </el-form-item>

        <el-button
          type="primary"
          @click="register"
        >注册</el-button>
      </el-form>
    </div>
    <div>
      <!-- <Camera
        class="mask"
        ref="camera"
        :show_mask="show_camera"
        @click.native="close_camera"
      /> -->
    </div>
  </div>
</template>

<script>
// import Camera from '@/components/Camera.vue';

export default {
  data() {
    return {
      show_camera: 'true',
      username: '',
      password: '',
    };
  },
  components: {
    // Camera,
  },
  methods: {
    register() {
      // console.log('register operate');
    },
    close_camera() {
      this.$refs.Camera.mediaStream.getVideoTracks()[0].stop();
      this.show_camera = false;
    },
  },
};
</script>

<style lang="less" scoped>
.mask {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}
.login-container {
  width: 500px;
  margin: 100px auto;
  border: 1px solid #ccc;
  border-radius: 10px;
  padding: 30px;
  box-shadow: 0 0 10px #ccc;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.title {
  font-size: 24px;
  font-weight: bold;
  padding-bottom: 15px;
}
</style>
