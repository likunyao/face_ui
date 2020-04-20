<template>
  <el-table
    :data="records"
    stripe
    style="width: 100%"
  >
    <el-table-column
      prop="date"
      label="日期"
      width="180"
    >
    </el-table-column>
    <el-table-column
      prop="name"
      label="姓名"
      width="180"
    >
    </el-table-column>
    <el-table-column
      prop="remark"
      label="备注"
    >
    </el-table-column>
  </el-table>
</template>

<script>
export default {
  props: ['records'],
};
</script>
