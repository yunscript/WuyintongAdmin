<template>
  <div class="app-container">
    <p>用户基本信息</p>
    <el-row :gutter="20">
      <el-col :span="21">
            <el-row :gutter="20" class="margin-bottom10">
              <el-col :span="10" class="mb20">
                <el-row>
                  <el-col :span="8" class="text-right">
                    用户名：
                  </el-col>
                  <el-col :span="16" class="text-left">
                    <el-input placeholder=""></el-input>
                  </el-col>
                </el-row>
              </el-col>
              <el-col :span="10" class="mb20">
                <el-row>
                  <el-col :span="8" class="text-right">
                    初始密码：
                  </el-col>
                  <el-col :span="16" class="text-left">
                    <el-input width='100' placeholder="请输入内容">
                    </el-input>
                  </el-col>
                </el-row>
              </el-col>
              <el-col :span="10" class="mb20">
                <el-row>
                  <el-col :span="8" class="text-right">
                    姓名：
                  </el-col>
                  <el-col :span="16" class="text-left">
                    <el-input placeholder=""></el-input>
                  </el-col>
                </el-row>
              </el-col>
              <el-col :span="10" class="mb20">
                <el-row>
                  <el-col :span="8" class="text-right">
                    职位：
                  </el-col>
                  <el-col :span="16" class="text-left">
                    <el-input placeholder=""></el-input>
                  </el-col>
                </el-row>
              </el-col>
              <el-col :span="10" class="mb20">
                <el-row>
                  <el-col :span="8" class="text-right">
                    联系方式：
                  </el-col>
                  <el-col :span="16" class="text-left">
                    <el-input placeholder=""></el-input>
                  </el-col>
                </el-row>
              </el-col>
              <el-col :span="10" class="mb20">
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
              <el-col :span="10" class="mb20">
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
    <div class="checkbox margin-bottom10">
      <el-checkbox v-model="homeChecked">首页</el-checkbox>
    </div>
    <div class="checkbox margin-bottom10">
      <el-checkbox v-model="trade.selectAll" @change="handleCheckAllChange(trade.selectAll, )">{{ trade.oneLable}}</el-checkbox>
      <el-row class='ml15'>
        <el-col :span="6" v-for="(items, index) in trade.financeManagement">
          <div class="mt10">
            <el-checkbox v-model="items.selectAll" @change="handleCheckAllChange(items.selectAll, items.checkedCities, items.twoLable)">{{ items.oneLable }}</el-checkbox>
            <div style="margin: 15px 0;"></div>
            <el-checkbox-group v-model="items.checkedCities" @change="handleCheckedCitiesChange('selectAll', index, items.twoLable, items.checkedCities)">
              <el-checkbox class='ml15 block mb10' v-for="city in items.twoLable" :label="city" :key="city">{{city}}</el-checkbox>
            </el-checkbox-group>
          </div>
        </el-col>
      </el-row>
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
      homeChecked: false,
      financeChecked: false,
      trade: {
        oneLable: '融资管理', //  一级选项
        // twoLable: ['融资申请', '授信管理', '用款查询', '还款查询'],
        checkedCities: ['融资申请'],
        selectAll: false,
        financeManagement: [{
          oneLable: '融资申请', //  一级选项
          twoLable: ['正在审批', '审批记录', '授信批复', '查看企业信息', '修改授信批复', '授信审核', '查看审批记录'], //  二级选项
          checkedCities: ['正在审批', '审批记录'], //  默认选中
          selectAll: false  //  一级全选控制按钮
        }, {
          oneLable: '授信管理',
          twoLable: ['查看授信详情'],
          checkedCities: ['查看授信详情'],
          selectAll: true  //  一级全选控制按钮
        }, {
          oneLable: '用款查询',
          twoLable: ['查看用款详情', '放款确认', '查看放款凭证'],
          checkedCities: ['查看用款详情', '查看放款凭证'],
          selectAll: false
        }, {
          oneLable: '还款查询',
          twoLable: ['账单明细', '还款详情'],
          checkedCities: ['还款详情'],
          selectAll: false  //  一级全选控制按钮
        }]
      },
      financeManagement: [{
        oneLable: '融资申请', //  一级选项
        twoLable: ['正在审批', '审批记录', '授信批复', '查看企业信息', '修改授信批复', '授信审核', '查看审批记录'], //  二级选项
        checkedCities: ['正在审批', '审批记录'], //  默认选中
        selectAll: false  //  一级全选控制按钮
      }, {
        oneLable: '授信管理',
        twoLable: ['查看授信详情'],
        checkedCities: ['查看授信详情'],
        selectAll: true  //  一级全选控制按钮
      }, {
        oneLable: '用款查询',
        twoLable: ['查看用款详情', '放款确认', '查看放款凭证'],
        checkedCities: ['查看用款详情', '查看放款凭证'],
        selectAll: false
      }, {
        oneLable: '还款查询',
        twoLable: ['账单明细', '还款详情'],
        checkedCities: ['还款详情'],
        selectAll: false  //  一级全选控制按钮
      }]
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    handleCheckAllChange(selectAll, checkedOptions, options) {
      checkedOptions.splice(0, checkedOptions.length)
      if (selectAll) {
        options.forEach((item, i) => {
          this.$set(checkedOptions, i, options[i])
        })
      }
    },
    handleCheckedCitiesChange(checkAll, index, options, checkedOptions) {
      const checkedCount = checkedOptions.length
      this.$set(this.trade.financeManagement[index], checkAll, checkedCount === options.length)
    },
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
.mb20 {
  margin-bottom: 20px;
}
.mb10 {
  margin-bottom: 10px;
}
.mt10 {
  margin-top: 10px;
}
.ml15 {
  margin-left: 15px;
}
</style>
