<template>
  <div class="login form">
    <h4>注册</h4>
    <br>
    <el-form :model="registerForm" :rules="rules" ref="registerForm" label-width="100px" @submit.native.prevent>
      <el-form-item label="邮箱" prop="username">
        <el-input v-model="registerForm.username" size="small"></el-input>
      </el-form-item>
      <el-form-item label="密码" prop="password">
        <el-input v-model="registerForm.password" type="password" size="small"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" native-type="submit" :loading="loading" @click="submitForm('registerForm')" size="small" style="margin-right:2rem;">立即注册</el-button>
        <el-button @click="goLogin" size="small">去登录</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
  import { Auth } from 'aws-amplify';
  export default {
    name: 'Register',
    data() {
      return {
        registerForm: {
          username: '',
          password: '',
        },
        loading:false,
        rules: {
          username: [
            { required: true, message: '请输入邮箱', trigger: 'blur' },
          ],
          password: [
            { required: true, message: '请输入密码', trigger: 'blur' }
          ],
        }
      };
    },
    created(){
      this.registerForm.username = this.$route.query.username??'';
    },
    methods: {
      goLogin(){
        let { username } = this.registerForm;
        this.$router.push({path:'/login',query:{username}});
      },
      async signUp() {
        this.loading = true;
        let { username,password } = this.registerForm;
        try {
          const { user } = await Auth.signUp({
              username,
              password,
          });
          console.log(user);
          this.loading = false;
          this.$message.success('sign up success');
          this.$router.push({path:'/confirm',query:{username}})
        } catch (error) {
            console.log('error signing up:', error);
            this.$message.error(error);
            this.loading = false;
        }
      },
      async submitForm(formName) {
        this.$refs[formName].validate(async (valid) => {
          if (valid) {
            await this.signUp();
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
