<template>
  <div class="login-container">
    <h1 class="title">登陆</h1>
    <el-form
      label-position="left"
      label-width="20%"
    >
      <el-form-item label="用户名">
        <el-input v-model="username"></el-input>
      </el-form-item>
      <el-form-item label="密码">
        <el-input
          @keydown.native.enter="login"
          show-password
          v-model="password"
        ></el-input>
      </el-form-item>
      <el-button
        type="primary"
        @click="login"
        style="float: center"
      >登录</el-button>
      <div class="register-container">
        <router-link
          to="/Register"
          style="text-decoration: none"
        >注册</router-link>
      </div>
    </el-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: '',
      password: '',
    };
  },
  methods: {
    login() {
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
        this.$axios.post('http://127.0.0.1:8000/login', data)
          .then((res) => {
            if (res.data.success === true) {
              this.$message({
                message: '登录成功!',
                type: 'success',
              });
              this.$router.push({ path: '/Home' });
            }
          })
          .catch((err) => {
            this.$message({
              message: err,
              type: 'warning',
            });
          });
      }
    },
  },
};
</script>

<style lang="less" scoped>
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
.register-container {
  float: right;
}
</style>
