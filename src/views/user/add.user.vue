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
      <el-checkbox v-model="financeChecked">金融产品管理</el-checkbox>
      <el-row class='ml15'>
        <el-col :span="6">
          <div class="mt10">
            <el-checkbox v-model="selectAll.addPersonLoanSelectAll" @change="handleCheckAllChange(selectAll.addPersonLoanSelectAll, checkedCities, cities)">全选</el-checkbox>
            <div style="margin: 15px 0;"></div>
            <el-checkbox-group v-model="checkedCities" @change="handleCheckedCitiesChange('addPersonLoanSelectAll', cities, checkedCities)">
              <el-checkbox class='ml15 block mb10' v-for="city in cities" :label="city" :key="city">{{city}}</el-checkbox>
            </el-checkbox-group>
          </div>
        </el-col>
        <el-col :span="6">
          <div class="mt10">
            <el-checkbox v-model="checkAll">全选</el-checkbox>
            <div style="margin: 15px 0;"></div>
            <el-checkbox-group v-model="checkedCities" @change="handleCheckedCitiesChange">
              <el-checkbox class='ml15 block mb10' v-for="city in cities" :label="city" :key="city">{{city}}</el-checkbox>
            </el-checkbox-group>
          </div>
        </el-col>
        <el-col :span="6">
          <div class="mt10">
            <el-checkbox v-model="checkAll">全选</el-checkbox>
            <div style="margin: 15px 0;"></div>
            <el-checkbox-group v-model="checkedCities" @change="handleCheckedCitiesChange">
              <el-checkbox class='ml15 block mb10' v-for="city in cities" :label="city" :key="city">{{city}}</el-checkbox>
            </el-checkbox-group>
          </div>
        </el-col>
        <el-col :span="6">
          <div class="mt10">
            <el-checkbox v-model="checkAll">全选</el-checkbox>
            <div style="margin: 15px 0;"></div>
            <el-checkbox-group v-model="checkedCities" @change="handleCheckedCitiesChange">
              <el-checkbox class='ml15 block mb10' v-for="city in cities" :label="city" :key="city">{{city}}</el-checkbox>
            </el-checkbox-group>
          </div>
        </el-col>
      </el-row>
    </div>
  </div>
</template>
<script>
import { fetchList } from '@/api/article'
const cityOptions = ['上海', '北京', '广州', '深圳']

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
      checkAll: true,
      selectAll: {
        addPersonLoanSelectAll: false
      },
      checkedCities: ['上海', '北京'],
      cities: cityOptions,
      isIndeterminate: true
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    handleCheckAllChange(selectAll, checkedOptions, options) {
      if (selectAll) {
        checkedOptions.splice(0, checkedOptions.length)
        for (var i = 0; i < options.length; i++) {
          checkedOptions.push(options[i])
        }
      } else {
        checkedOptions = checkedOptions.splice(0, checkedOptions.length)
      }
    },
    handleCheckedCitiesChange(checkAll, options, checkedOptions) {
      const checkedCount = checkedOptions.length
      // Vue.set(object, key, value)
      if (checkedCount === options.length) {
        this.$set(this.selectAll, checkAll, true)
      } else {
        this.$set(this.selectAll, checkAll, false)
      }
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
