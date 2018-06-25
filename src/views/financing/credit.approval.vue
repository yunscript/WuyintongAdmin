<template>
  <admin-dialog v-if="creditApproval.visible" :visible="creditApproval.visible" :title="creditApproval.dialogTitle" v-on:updateVisible="updateVisible">
    <div slot="main">
      <el-row>
        <el-col :span="10" style="text-align: right;">
          是否同意授信：
        </el-col>
        <el-col :span="12" style="text-align: left;">
          <el-radio v-model="radio" label="1">同意</el-radio>
          <el-radio v-model="radio" label="2">拒绝</el-radio>
        </el-col>
      </el-row>

      <div v-if='radio == "1"' class="">

        <el-row>
          <el-col :span="10" style="text-align: right;">
            企业名称：
          </el-col>
          <el-col :span="12" style="text-align: left;">
            <el-input placeholder=""></el-input>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="10" style="text-align: right;">
            产品名称：
          </el-col>
          <el-col :span="12" style="text-align: left;">
            <el-select v-model="value" placeholder="请选择">
              <el-option
                v-for="item in options"
                :key="item.value"
                :label="item.label"
                :value="item.value">
              </el-option>
            </el-select>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="10" style="text-align: right;">
            授信额度（元）：
          </el-col>
          <el-col :span="12" style="text-align: left;">
            <el-input placeholder=""></el-input>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="10" style="text-align: right;">
            授信利率：
          </el-col>
          <el-col :span="12" style="text-align: left;">
            <el-input placeholder=""></el-input>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="10" style="text-align: right;">
            授信起始日：
          </el-col>
          <el-col :span="12" style="text-align: left;">
            <el-date-picker
              v-model="value1"
              type="date"
              placeholder="选择日期">
            </el-date-picker>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="10" style="text-align: right;">
            授信截止日：
          </el-col>
          <el-col :span="12" style="text-align: left;">
            <el-date-picker
              v-model="value1"
              type="date"
              placeholder="选择日期">
            </el-date-picker>
          </el-col>
        </el-row>
      </div>
      <div v-if='radio == "2"' class="">
        <el-row>
          <el-col :span="10" style="text-align: right;">
            原因：
          </el-col>
          <el-col :span="12" style="text-align: left;">
            <el-input
              type="textarea"
              :rows="2"
              :autosize="{ minRows: 2, maxRows: 4}"
              placeholder="请输入内容"
              v-model="textarea">
            </el-input>
          </el-col>
        </el-row>
      </div>
      <div slot="footer" class="dialog-footer">
        <el-button  @click="updateVisible">取 消</el-button>
        <el-button type="primary" @click="">确 定</el-button>
      </div>
    </div>
  </admin-dialog>
</template>
<script>
export default {
  data() {
    return {
      radio: '',
      options: [{
        value: '选项1',
        label: '黄金糕'
      }, {
        value: '选项2',
        label: '双皮奶'
      }, {
        value: '选项3',
        label: '蚵仔煎'
      }, {
        value: '选项4',
        label: '龙须面'
      }, {
        value: '选项5',
        label: '北京烤鸭'
      }],
      value: '',
      value1: '',
      textarea: ''
    }
  },
  props: {
    creditApproval: {
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
    updateVisible() {
      this.$emit('updateVisible', false)
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
</style>
