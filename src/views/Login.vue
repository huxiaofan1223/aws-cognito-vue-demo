<template>
  <div class="login form">
    <h4>登录</h4>
    <br>
    <el-form :model="loginForm" :rules="rules" ref="loginForm" label-width="100px" @submit.native.prevent>
      <el-form-item label="邮箱" prop="username">
        <el-input v-model="loginForm.username" size="small"></el-input>
      </el-form-item>
      <el-form-item label="密码" prop="password">
        <el-input v-model="loginForm.password" type="password" size="small"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" native-type="submit" @click="submitForm('loginForm')" :loading="loading" size="small" style="margin-right:2rem;">登录</el-button>
        <el-button @click="goRegister" size="small">去注册</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
  import { Auth } from 'aws-amplify';
  export default {
    name: 'Login',
    data() {
      return {
        loginForm: {
          username: '',
          password: ''
        },
        loading:false,
        rules: {
          username: [
            { required: true, message: '请输入邮箱', trigger: 'blur' },
          ],
          password: [
            { required: true, message: '请输入密码', trigger: 'blur' }
          ]
        }
      };
    },
    created(){
      this.loginForm.username = this.$route.query.username??'';
    },
    methods: {
      goRegister(){
        let { username } = this.loginForm;
        this.$router.push({path:'/register',query:{username}});
      },
      async login(){
        this.loading = true;
        try {
          let { username ,password } = this.loginForm;
          const res = await Auth.signIn({
              username,
              password,
          });
          localStorage.setItem('token',res.signInUserSession.accessToken.jwtToken)
          this.loading = false;
          this.$message.success('sign in success');
          this.$router.push({path:'/'});
        } catch (error) {
            console.log('error signing up:', error);
            this.$message.error(error);
            this.loading =false;
        }
      },
      submitForm(formName) {
        this.$refs[formName].validate(async(valid) => {
          if (valid) {
            this.login();
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      },
      resetForm(formName) {
        this.$refs[formName].resetFields();
      }
    }
  }
</script>
