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
      <el-col :span="20">
        <div class="pro-container">
          <el-row :gutter="20">
            <el-col :span="16">
              <div class="demo-input-suffix">
                产品说明：
                <el-input
                  class='w_60'
                  type="textarea"
                  :rows="5"
                  placeholder="请输入内容"
                  v-model="productDescription">
                </el-input>
              </div>
            </el-col>
            <el-col :span="8">
              product logo
            </el-col>

          </el-row>
          <el-row>
            <el-col :span="16">
              <div class="">
                产品渠道
                <el-tag
                    :key="tag"
                    v-for="tag in dynamicTags"
                    closable
                    :disable-transitions="false"
                    @close="handleClose(tag)">
                    {{tag}}
                </el-tag>
                <el-input
                  class="input-new-tag"
                  v-if="inputVisible"
                  v-model="inputValue"
                  ref="saveTagInput"
                  size="small"
                  @keyup.enter.native="handleInputConfirm"
                  @blur="handleInputConfirm"
                  >
                </el-input>
                <el-button v-else class="button-new-tag" size="small" @click="showInput">+ New Tag</el-button>
              </div>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="16">
              <div class="">
                产品合同
                <el-tag
                    :key="tag"
                    v-for="tag in dynamicTags"
                    closable
                    :disable-transitions="false"
                    @close="handleClose(tag)">
                    {{tag}}
                </el-tag>
                <el-input
                  class="input-new-tag"
                  v-if="inputVisible"
                  v-model="inputValue"
                  ref="saveTagInput"
                  size="small"
                  @keyup.enter.native="handleInputConfirm"
                  @blur="handleInputConfirm"
                  >
                </el-input>
                <el-button v-else class="button-new-tag" size="small" @click="showInput">+ New Tag</el-button>
              </div>
            </el-col>
          </el-row>
          <div slot="footer" class="dialog-footer">
            <el-button>取 消</el-button>
            <el-button type="primary">确 定</el-button>
          </div>
        </div>
        <el-row :gutter="20">
          <el-col :span="12">
            <div class="grid-content bg-purple">
              <!-- <h2>个人信息</h2>
              <p>标准项</p> -->
dedd
            </div>
          </el-col>
          <el-col :span="12" :offset="6">
            <div class="grid-content bg-purple">说不定是大百货商店</div>
          </el-col>
          <!-- <el-col :span="12" :offset="6"><div class="grid-content bg-purple">基督山伯爵的</div></el-col>
          <el-col :span="12" :offset="6"><div class="grid-content bg-purple">十点半结束的</div></el-col> -->
        </el-row>
      </el-col>
    </div>
  </el-row>
</div>
</template>

<script>
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
      },
      productDescription: '',
      dynamicTags: ['物银通', '全链发布', '侧链'],
      inputVisible: false,
      inputValue: ''
    }
  },
  methods: {
    showCreatedTimes() {
      this.createdTimes = this.createdTimes + 1
    },
    handleModifyStatus() {
      this.createUser.visible = true
    },
    handleClose(tag) {
      this.dynamicTags.splice(this.dynamicTags.indexOf(tag), 1)
    },
    showInput() {
      this.inputVisible = true
      this.$nextTick(_ => {
        this.$refs.saveTagInput.$refs.input.focus()
      })
    },
    handleInputConfirm() {
      const inputValue = this.inputValue
      if (inputValue) {
        this.dynamicTags.push(inputValue)
      }
      this.inputVisible = false
      this.inputValue = ''
    }
  },
  components: {

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
.w_60 {
  width: 60%;
}
.el-col {
  margin: 5px 0;
}
.bg-purple {
  background-color: tan;
}

.bg-gray {
  background-color: #eee;
}
.el-tag {
  margin: 0 5px;
}
</style>
