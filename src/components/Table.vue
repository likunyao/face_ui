<template>
  <el-table
    :data="records"
    stripe
    style="width: 100%"
    :default-sort="{prop: 'date', order: 'ascending'}"
  >
    <el-table-column
      prop="date"
      label="日期"
      sortable
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
