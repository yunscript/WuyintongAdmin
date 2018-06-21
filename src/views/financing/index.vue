<template>
  <div class="app-container">
    <el-row>
      <el-col :span="3">
        <!-- 步骤条 -->
        <el-steps direction="vertical" :space="100" :active="1" finish-status="success">
          <el-step title="融资申请"></el-step>
          <el-step title="授信初审"></el-step>
          <el-step title="授信复审"></el-step>
          <el-step title="授信启用"></el-step>
          <el-step title="授信到期"></el-step>
        </el-steps>
      </el-col>
      <el-col :span="21">
        <el-button style='margin-bottom:20px' type="primary" icon="document" @click="handleDownload" :loading="downloadLoading">导出已选择项</el-button>
        <el-table :data="list" v-loading.body="listLoading" element-loading-text="拼命加载中" border fit highlight-current-row @selection-change="handleSelectionChange"
        ref="multipleTable">
        <el-table-column type="selection" align="center"></el-table-column>
        <el-table-column align="center" label='融资申请编号' width="95">
          <template scope="scope">
            {{scope.$index}}
          </template>
        </el-table-column>
        <el-table-column label="企业名称">
          <template scope="scope">
            {{scope.row.title}}
          </template>
        </el-table-column>
        <el-table-column label="产品名称" width="95" align="center">
          <template scope="scope">
            <el-tag>{{scope.row.author}}</el-tag>
          </template>
        </el-table-column>
        <el-table-column label="申请时间" width="115" align="center">
          <i class="el-icon-time"></i>
          <template scope="scope">
            {{scope.row.display_time}}
          </template>
        </el-table-column>
        <el-table-column label="初审时间" width="115" align="center">
          <i class="el-icon-time"></i>
          <template scope="scope">
            {{scope.row.display_time}}
          </template>
        </el-table-column>
        <el-table-column label="复审时间" width="115" align="center">
          <i class="el-icon-time"></i>
          <template scope="scope">
            {{scope.row.display_time}}
          </template>
        </el-table-column>
        <el-table-column align="center" prop="created_at" label="状态" width="100">
          <template scope="scope">
            <span>{{scope.row.pageviews}}</span>
          </template>
        </el-table-column>
        <el-table-column align="center" prop="created_at" label="备注" width="100">
          <template scope="scope">
            <span>{{scope.row.pageviews}}</span>
          </template>
        </el-table-column>
        <el-table-column
          label="操作"
          width="100">
          <template scope="scope">
            <el-button @click="handleClick(scope.row)" type="text" size="small">查看</el-button>
            <el-button @click="handleClick(scope.row)" type="text" size="small">编辑</el-button>
          </template>
        </el-table-column>
      </el-table>
      <div class="block">
      <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page="currentPage"
        :page-sizes="[100, 200, 300, 400]"
        :page-size="100"
        layout="total, sizes, prev, pager, next, jumper"
        :total="400">
      </el-pagination>
    </div>
      </el-col>
    </el-row>
    <!-- 分页  -->
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
      currentPage: 1
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    handleClick(row) {
      console.log(row)
    },
    handleSizeChange(val) {
      // console.log(`每页 ${val} 条`);
    },
    handleCurrentChange(val) {
      // console.log(`当前页: ${val}`);
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
