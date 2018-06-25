<template>
<div class="management-container">
  <el-row :gutter="20">
    <el-col :span="4">
      <el-menu>
        <el-menu-item-group>
          <template slot="title">个人贷款</template>
          <el-menu-item index="1-1">个人信息</el-menu-item>
          <el-menu-item index="1-2">个人车辆信息</el-menu-item>
        </el-menu-item-group>
      </el-menu>
    </el-col>
    <div class="">
      <el-col :span="20">
        <div class="pro-container">
          <el-row :gutter="20">
            <el-col :span="8">
              <div class="demo-input-suffix">
                产品名称：
                <el-input placeholder="">
                </el-input>
              </div>
            </el-col>
            <el-col :span="8">
              <div class="grid-content bg-purple"></div>
              <div class="demo-input-suffix">
                产品年化利率：
                <el-input class="rate" placeholder="">
                </el-input>% -
                <el-input class="rate" placeholder="">
                </el-input>%
              </div>
            </el-col>
            <el-col :span="8">
              <div class="demo-input-suffix">
                授信期限：
                <el-select v-model="value" placeholder="请选择">
                  <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
                  </el-option>
                </el-select>
              </div>
            </el-col>
          </el-row>
        </div>
      </el-col>
      <el-col :span="20">
        <div class="pro-container">
          <el-row :gutter="20">
            <el-col :span="8">
              <div class="demo-input-suffix">
                还款方式：
                <el-input placeholder="">
                </el-input>
              </div>
            </el-col>
            <el-col :span="8">
              <div class="grid-content bg-purple"></div>
              <div class="demo-input-suffix">
                贷款额度范围：
                <el-input class="rate" placeholder="">
                </el-input>% -
                <el-input class="rate" placeholder="">
                </el-input>%
              </div>
            </el-col>
            <el-col :span="8">
              <div class="demo-input-suffix">
                用款周期：
                <el-select v-model="value" placeholder="请选择">
                  <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
                  </el-option>
                </el-select>
              </div>
            </el-col>
          </el-row>
        </div>
      </el-col>
    </div>
  </el-row>
  <el-button size="small" type="primary" icon="el-icon-edit" v-waves @click="handleModifyStatus()">编辑</el-button>

  <create-user :createUser="createUser" v-on:updateVisible="updateVisible"></create-user>
</div>
</template>

<script>
import CreateUser from './user.create.vue'
import waves from '@/directive/waves/index.js' // 水波纹指令

export default {
  name: 'tabDemo',
  directives: {
    waves
  },
  data() {
    return {
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
      createUser: {
        dialogTitle: '授信初审批复',
        visible: false
      }
    }
  },
  methods: {
    showCreatedTimes() {
      this.createdTimes = this.createdTimes + 1
    },
    updateVisible(flag) {
      this.createUser.visible = flag
    },
    handleModifyStatus() {
      this.createUser.visible = true
    }
  },
  components: {
    CreateUser
  }
}
</script>

<style scoped>
.management-container {
  margin: 30px;
}

.el-input {
  width: 200px;
}

.rate {
  width: 80px;
}

.bg-purple {
  background-color: tan;
}

.bg-gray {
  background-color: #eee;
}
</style>
