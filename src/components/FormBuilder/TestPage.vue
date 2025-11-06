<template>
  <div>
    <el-row :gutter="15">
      <el-form ref="elForm" :model="formData" :rules="rules" size="medium" label-width="100px"
        label-position="left">
        <el-col :span="12">
          <el-form-item label="手机号" prop="mobile">
            <el-select v-model="formData.mobile" placeholder="请输入手机号" clearable :style="{width: '100%'}">
              <el-option v-for="(item, index) in mobileOptions" :key="index" :label="item.label"
                :value="item.value" :disabled="item.disabled"></el-option>
            </el-select>
          </el-form-item>
        </el-col>
        <el-col :span="17">
          <el-form-item label="单行文本" prop="field104">
            <el-input v-model="formData.field104" placeholder="请输入单行文本" clearable :style="{width: '100%'}">
            </el-input>
          </el-form-item>
        </el-col>
        <el-col :span="10">
          <el-form-item label="密码" prop="field105">
            <el-input v-model="formData.field105" placeholder="请输入密码" clearable show-password
              :style="{width: '100%'}"></el-input>
          </el-form-item>
        </el-col>
        <el-col :span="17">
          <el-form-item label="评分" prop="field106">
            <el-rate v-model="formData.field106"></el-rate>
          </el-form-item>
        </el-col>
        <el-col :span="17">
          <el-form-item label="上传" prop="field107" required>
            <el-upload ref="field107" :file-list="field107fileList" :action="field107Action"
              :before-upload="field107BeforeUpload">
              <el-button size="small" type="primary" icon="el-icon-upload">点击上传</el-button>
            </el-upload>
          </el-form-item>
        </el-col>
        <el-col :span="17">
          <el-form-item label="按钮" prop="field108">
            <el-button type="primary" icon="el-icon-search" size="medium"> 主要按钮 </el-button>
          </el-form-item>
        </el-col>
        <el-col :span="6">
          <el-row gutter="15">
            <el-col :span="12">
              <el-form-item label="按钮" prop="field110">
                <el-button type="primary" icon="el-icon-search" size="medium"> 主要按钮 </el-button>
              </el-form-item>
            </el-col>
          </el-row>
        </el-col>
        <el-col :span="24">
          <el-form-item size="large">
            <el-button type="primary" @click="submitForm">提交</el-button>
            <el-button @click="resetForm">重置</el-button>
          </el-form-item>
        </el-col>
      </el-form>
    </el-row>
  </div>
</template>
<script>
export default {
  components: {},
  props: [],
  data() {
    return {
      formData: {
        mobile: 1,
        field104: undefined,
        field105: undefined,
        field106: 4,
        field107: null,
        field108: undefined,
        field110: undefined,
      },
      rules: {
        mobile: [{
          required: true,
          message: '请输入手机号',
          trigger: 'change'
        }, {
          pattern: /^1(3|4|5|7|8|9)\d{9}$/,
          message: '手机号格式错误',
          trigger: 'change'
        }],
        field104: [{
          required: true,
          message: '请输入单行文本',
          trigger: 'blur'
        }],
        field105: [{
          required: true,
          message: '请输入密码',
          trigger: 'blur'
        }],
        field106: [{
          required: true,
          message: '评分不能为空',
          trigger: 'change'
        }],
      },
      field107Action: 'https://jsonplaceholder.typicode.com/posts/',
      field107fileList: [],
      mobileOptions: [{
        "label": "选项一",
        "value": 1
      }, {
        "label": "选项二",
        "value": 2
      }],
    }
  },
  computed: {},
  watch: {},
  created() {},
  mounted() {},
  methods: {
    submitForm() {
      this.$refs['elForm'].validate(valid => {
        if (!valid) return
        // TODO 提交表单
      })
    },
    resetForm() {
      this.$refs['elForm'].resetFields()
    },
    field107BeforeUpload(file) {
      let isRightSize = file.size / 1024 / 1024 < 2
      if (!isRightSize) {
        this.$message.error('文件大小超过 2MB')
      }
      return isRightSize
    },
  }
}

</script>
<style>
.el-rate {
  display: inline-block;
  vertical-align: text-top;
}

.el-upload__tip {
  line-height: 1.2;
}

</style>
