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
  </div>
</template>

<script>
// import Camera from '@/components/Camera.vue';

export default {
  data() {
    return {
      username: '',
      password: '',
    };
  },
  components: {
    // Camera,
  },
  methods: {
    register() {
      if (!this.username.trim() || !this.password.trim()) {
        this.$message({
          message: '请输入用户名和密码!',
          type: 'warning',
        });
      } else {
        const data = {
          username: this.username,
          password: this.password,
        };
        this.$axios.post('http://123.56.15.233:8000/register', data)
          .then((res) => {
            if (res.data.success === true) {
              this.$message({
                message: '注册成功!',
                type: 'success',
              });
              this.$router.push({ path: '/' });
            } else {
              this.$message({
                message: res.data.error,
                type: 'warning',
              });
            }
          })
          .catch((err) => {
            this.$message({
              mesage: err,
              type: 'warning',
            });
          });
      }
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
