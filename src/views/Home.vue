<template>
  <div class="home">
    <el-container>
      <el-header>
        <h1>Welcome to Face Recognition App</h1>
        <el-avatar
          class="user-icon"
          shape="square"
          icon="el-icon-user-solid"
        >
        </el-avatar>
      </el-header>
      <el-main>
        <Table v-bind:records="items"></Table>
      </el-main>
      <el-footer>
        <p class="foot">foot</p>
      </el-footer>
    </el-container>
  </div>
</template>

<script>
import Table from '@/components/Table.vue';

export default {
  name: 'Home',
  data() {
    return {
      items: [],
    };
  },
  components: {
    // HelloWorld,
    Table,
  },
  created() {
    this.$axios.get('http://127.0.0.1:8000/records')
      .then((res) => {
        if (res.data.success === true) {
          this.items = JSON.parse(res.data.data);
        }
      })
      .catch((err) => {
        this.$message({
          message: err,
          type: 'warning',
        });
      });
  },
};
</script>

<style>
.el-header {
  background-color: #eaeff7;
  color: #333;
  display: flex;
  justify-content: center;
  align-items: center;
}
.user-icon {
  justify-content: end;
  margin-left: auto;
}
.foot {
  text-align: center;
  vertical-align: bottom;
}
</style>
