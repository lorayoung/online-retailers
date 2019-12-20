<template>
  <div class="login-container">
    <div class="login_box">
      <div class="avatar_box">
        <img src="../assets/logo.png" alt>
      </div>
      <el-form
        label-width="0px"
        class="login_form"
        ref="loginBox"
        :model="loginForm"
        :rules="loginRules"
      >
        <el-form-item label prop="username">
          <el-input prefix-icon="iconfont icon-user" v-model="loginForm.username"></el-input>
        </el-form-item>
        <el-form-item label prop="password">
          <el-input
            prefix-icon="iconfont icon-3702mima"
            v-model="loginForm.password"
            type="password"
          ></el-input>
        </el-form-item>
        <el-form-item class="btns">
          <el-button type="primary" @click="submit('loginBox')">登录</el-button>
          <el-button type="info" @click="resetForm('loginBox')">重置</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'login',
  data () {
    return {
      loginForm: {
        username: '',
        password: ''
      },
      loginRules: {
        username: [
          { required: true, message: '请输入登录用户', trigger: 'blur' },
          { min: 3, max: 10, message: '长度在3到10个字符', trigger: 'blur' }
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 6, max: 15, message: '长度在6到15个字符', trigger: 'blur' }
        ]
      }
    }
  },
  components: {},
  created () {},
  mounted () {},
  methods: {
    // 表单重置
    resetForm (name) {
      this.$refs[name].resetFields()
    },
    // 表单登录
    submit (name) {
      this.$refs[name].validate(async valid => {
        if (valid) {
          const { data: res } = await this.$http.post('login', this.loginForm)
          if (res.meta.status !== 200) return this.$message.error(res.meta.msg)
          this.$message.success(res.meta.msg)
          // 将token存在sessrionstorage
          window.sessionStorage.setItem('token', res.data.token)
          this.$router.push('/home')
        }
      })
    }
  }
}
</script>
<style lang="less" scoped>
.login-container {
  background-color: #2b4b6b;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  .login_box {
    width: 450px;
    height: 300px;
    background-color: #fff;
    border-radius: 5px;
    position: relative;
    .avatar_box {
      width: 130px;
      height: 130px;
      border: 1px solid #eee;
      padding: 10px;
      border-radius: 50%;
      box-shadow: 0 0 10px #ddd;
      position: absolute;
      left: 50%;
      background-color: #fff;
      transform: translateX(-50%) translateY(-50%);
      img {
        height: 100%;
        width: 100%;
        border-radius: 50%;
        background-color: #eee;
      }
    }
    .btns {
      display: flex;
      justify-content: flex-end;
    }
    .login_form {
      padding: 0 20px;
      position: absolute;
      width: 100%;
      bottom: 0;
      box-sizing: border-box;
    }
  }
}
</style>
