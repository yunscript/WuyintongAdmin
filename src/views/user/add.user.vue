<template>
  <div class="app-container">
    <p>用户基本信息</p>
    <el-row :gutter="20">
      <el-col :span="21">
            <el-row :gutter="20" class="margin-bottom10">
              <el-col :span="10">
                <el-row>
                  <el-col :span="8" class="text-right">
                    用户名：
                  </el-col>
                  <el-col :span="16" class="text-left">
                    <el-input placeholder=""></el-input>
                  </el-col>
                </el-row>
              </el-col>
              <el-col :span="10">
                <el-row>
                  <el-col :span="8" class="text-right">
                    初始密码：
                  </el-col>
                  <el-col :span="16" class="text-left">
                    <el-input width='100' placeholder="请输入内容" class="input-with-select">
                    </el-input>
                  </el-col>
                </el-row>
              </el-col>
              <el-col :span="10">
                <el-row>
                  <el-col :span="8" class="text-right">
                    姓名：
                  </el-col>
                  <el-col :span="16" class="text-left">
                    <el-input placeholder=""></el-input>
                  </el-col>
                </el-row>
              </el-col>
              <el-col :span="10">
                <el-row>
                  <el-col :span="8" class="text-right">
                    职位：
                  </el-col>
                  <el-col :span="16" class="text-left">
                    <el-input placeholder=""></el-input>
                  </el-col>
                </el-row>
              </el-col>
              <el-col :span="10">
                <el-row>
                  <el-col :span="8" class="text-right">
                    联系方式：
                  </el-col>
                  <el-col :span="16" class="text-left">
                    <el-input placeholder=""></el-input>
                  </el-col>
                </el-row>
              </el-col>
              <el-col :span="10">
                <el-row>
                  <el-col :span="8" class="text-right">
                    角色：
                  </el-col>
                  <el-col :span="16" class="text-left">
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
              </el-col>
              <el-col :span="10">
                <el-row>
                  <el-col :span="8" class="text-right">
                    权限状态：
                  </el-col>
                  <el-col :span="16" class="text-left">
                    <el-radio v-model="permissionStatus" label="1">禁用</el-radio>
                    <el-radio v-model="permissionStatus" label="2">启用</el-radio>
                  </el-col>
                </el-row>
              </el-col>
            </el-row>
      </el-col>
    </el-row>
    <p>用户权限设置</p>
    <div class="checkbox">
      <el-checkbox v-model="checked">首页</el-checkbox>
    </div>
  </div>
</template>
<script>
import { fetchList } from '@/api/article'

export default {
  data() {
    return {
      list: null,
      listLoading: true,
      multipleSelection: [],
      downloadLoading: false,
      currentPage: 1,
      options: [{
        value: '全部',
        label: '全部'
      }, {
        value: '融资申请',
        label: '融资申请'
      }, {
        value: '授信初审',
        label: '授信初审'
      }, {
        value: '授信复审',
        label: '授信复审'
      }, {
        value: '退回初审',
        label: '退回初审'
      }, {
        value: '授信拒绝',
        label: '授信拒绝'
      }, {
        value: '授信启用',
        label: '授信启用'
      }, {
        value: '授信到期',
        label: '授信到期'
      }],
      value: '',
      permissionStatus: '',
      checked: false
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    //  原有页面方法
    fetchData() {
      this.listLoading = true
      fetchList(this.listQuery).then(response => {
        this.list = response.data.items
        this.listLoading = false
      })
    },
    handleSelectionChange(val) {
      this.multipleSelection = val
    },
    handleDownload() {
      if (this.multipleSelection.length) {
        this.downloadLoading = true
        require.ensure([], () => {
          const { export_json_to_excel } = require('vendor/Export2Excel')
          const tHeader = ['序号', '文章标题', '作者', '阅读数', '发布时间']
          const filterVal = ['id', 'title', 'author', 'pageviews', 'display_time']
          const list = this.multipleSelection
          const data = this.formatJson(filterVal, list)
          export_json_to_excel(tHeader, data, '列表excel')
          this.$refs.multipleTable.clearSelection()
          this.downloadLoading = false
        })
      } else {
        this.$message({
          message: '请至少选择一条记录',
          type: 'warning'
        })
      }
    },
    formatJson(filterVal, jsonData) {
      return jsonData.map(v => filterVal.map(j => v[j]))
    }
  }
}
</script>
<style scoped>
.el-input {
  width: 200px;
}
.el-select {
  width: 120px;
}
p {
  color: white;
  font-size: 14px;
}
.checkbox {
  background-color: #272D4A;
  padding: 20px;
}
</style>
