<template>
  <div class="contact">
    <h1>联系我</h1>
    <p>如有任何问题，请随时联系我。</p>
    <el-row type="flex" justify="center">
      <el-col :span="12">
        <el-form ref="form" :model="form" label-position="top" style="width: 100%" :rules="rules">
          <el-form-item label="姓名" prop="name">
            <el-input v-model="form.name" placeholder="请输入您的姓名"></el-input>
          </el-form-item>
          <el-form-item label="邮箱" prop="email">
            <el-input
                v-model="form.email"
                placeholder="请输入您的邮箱"
            ></el-input>
          </el-form-item>
          <el-form-item label="意见或建议" prop="message">
            <el-input
                type="textarea"
                v-model="form.message"
                placeholder="请输入您的意见或建议"
            ></el-input>
          </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="submitForm">提交</el-button>
          </el-form-item>
        </el-form>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {

  data() {
    return {
      form: {
        name: '',
        email: '',
        message: '',
      },
      rules: {
        name: [
          { required: true, message: '请输入姓名', trigger: 'blur' }
        ],
        email: [
          { required: true, message: '请输入邮箱', trigger: 'blur' },
          { type: 'email', message: '请输入正确的邮箱', trigger: 'blur' }
        ],
        message: [
          { required: true, message: '请输入意见或建议', trigger: 'change' }
        ]
      }
    }
  },
  methods: {
    submitForm() {
      this.$refs.form.validate((valid) => {
        if (valid) {
          // 表单校验通过,提交表单
          this.$message.success("提交成功，感谢你的建议!");
          setTimeout(() => {
            this.$router.go(0);
          },2000)
        } else {
          // 校验失败
        }
      })
    }
  },
};
</script>

<style scoped>
.contact {
  text-align: center;
  padding: 2rem;
}

.el-form {
  background-color: #fff;
  padding: 2rem;
  border-radius: 8px;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
}
</style>
