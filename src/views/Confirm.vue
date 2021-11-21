<template>
  <div class="login form">
    <h4>验证邮箱</h4>
    <br>
    <el-form :model="confirmForm" :rules="rules" ref="confirmForm" label-width="100px" @submit.native.prevent>
      <el-form-item label="邮箱" prop="username">
        <el-input v-model="confirmForm.username" size="small"></el-input>
      </el-form-item>
      <el-form-item label="验证码" prop="code">
        <el-input v-model="confirmForm.code" type="code" size="small"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" native-type="submit" @click="submitForm('confirmForm')" :loading="loading" size="small" style="margin-right:2rem;">验证邮箱</el-button>
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
        confirmForm: {
          username: '',
          code: ''
        },
        loading:false,
        rules: {
          username: [
            { required: true, message: '请输入邮箱', trigger: 'blur' },
          ],
          code: [
            { required: true, message: '请输入验证码', trigger: 'blur' }
          ]
        }
      };
    },
    created(){
      this.confirmForm.username = this.$route.query.username??'';
    },
    methods: {
      async login(){
        this.loading = true;
        try {
          let { username ,code } = this.confirmForm;
          const res = await Auth.confirmSignUp(username, code);
          this.loading = false;
          this.$message.success('verify code success');
          this.$router.push({path:'/login',query:{username}})
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