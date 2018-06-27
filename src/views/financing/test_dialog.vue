<template lang="html">
  <el-dialog
    title="提示"
    :visible.sync="testDialog.visible"
    width="30%"
    >
    <span>{{ testDialog.title}}</span>
    <span slot="footer" class="dialog-footer">
      <el-button @click="testDialog.visible = false">取 消</el-button>
      <el-button type="primary" @click="testDialog.visible = false">确 定</el-button>
    </span>
  </el-dialog>
</template>

<script>
export default {
  data() {
    return {
      dialogVisible: false
    }
  },
  props: {
    testDialog: {
      type: Object
    }
  },
  methods: {
    updateVisible() {
      console.log('=====sdsd======')
    }
  }
}
</script>

<style lang="css">
</style>
