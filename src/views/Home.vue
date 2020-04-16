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
        <Table v-bind="item"></Table>
      </el-main>
      <el-footer>
        <p class="foot">foot</p>
      </el-footer>
    </el-container>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue';
import Table from '@/components/Table.vue';

export default {
  name: 'Home',
  data() {
    return {
      item: {
        date: '2016-05-02',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄',
      },
    };
  },
  components: {
    // HelloWorld,
    Table,
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
