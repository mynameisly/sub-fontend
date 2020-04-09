<template>
  <el-pagination
    align="center"
    background
    layout="sizes,prev, pager, next,jumper"
    :total="total"
    :current-page.sync="page.currentPage"
    :page-size.sync="page.pageSize"
    :page-sizes="[5, 10, 30]"
    @size-change="handleSizeChange"
    @current-change="handleCurrentChange"
  />
</template>
<script>
export default {
  name: 'Pagination',
  props: {
    total: {
      required: true,
      type: Number
    },
    page: {
      required: true,
      type: Object
    }
  },
  methods: {
    handleSizeChange (val) {
      this.page.pageSize = val
      this.$emit('pageChange', this.page)
    },
    handleCurrentChange (val) {
      this.page.currentPage = val
      this.$emit('pageChange', this.page)
    }
  }
}
</script>

<style lang="scss">
  .el-pagination {
    padding: 15px 5px;
  }
  .el-pagination.is-background .el-pager li:not(.disabled).active {
    background-color: #BE392A;
  }
  .el-select-dropdown__item.selected {
    color: #BE392A;
  }
</style>
