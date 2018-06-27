<template>
  <admin-dialog v-if="approvalRecord.visible" :visible="approvalRecord.visible" :title="approvalRecord.dialogTitle" v-on:recordVisible="recordVisible">
    <div slot="main">
      <el-table
        highlight-current-row
        :data="tableData"
        style="width: 100%">
        <el-table-column
          type="index"
          width="50"
          align="left">
        </el-table-column>
        <el-table-column
          prop="date"
          label="审批项"
          width="180"
          align="left">
        </el-table-column>
        <el-table-column
          prop="name"
          label="审批结果"
          width="180"
          align="left">
        </el-table-column>
        <el-table-column
          prop="name"
          label="审核人"
          width="180"
          align="left">
        </el-table-column>
        <el-table-column
          prop="name"
          label="审核时间"
          width="180"
          align="left">
        </el-table-column>
        <el-table-column
          prop="备注"
          label="地址"
          align="left">
        </el-table-column>
      </el-table>
      <div slot="footer" class="dialog-footer">
        <el-button type="primary" @click="recordVisible">关 闭</el-button>
      </div>
    </div>
  </admin-dialog>
</template>
<script>
export default {
  data() {
    return {
      tableData: [{
        date: '2016-05-02',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        date: '2016-05-04',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1517 弄'
      }, {
        date: '2016-05-01',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1519 弄'
      }, {
        date: '2016-05-03',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1516 弄'
      }]
    }
  },
  props: {
    approvalRecord: {
      type: Object
    }
  },
  // created() {
  // },
  // computed: {
  //
  // },
  // watch: {
  //
  // },
  methods: {
    recordVisible() {
      this.$emit('recordVisible', false)
    }
  }
}
</script>
<style media="screen">
.el-row {
  margin-bottom: 10px;
}
.el-input {
  width: 200px;
}
.dialog-footer {
  margin-top: 20px;
}
.main {
  margin: 10px;
}
/*.el-table {
  height: 100px;
  overflow: auto;
}*/
</style>
