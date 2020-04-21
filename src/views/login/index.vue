<template>
  <div id="login">
    <div class="reg_container">
      <el-form ref="form" :model="form" :rules="rules" label-width="60px">
        <h1>用户登录</h1>
        <el-form-item label="用户名">
          <el-input v-model="form.username" placeholder="长度在6-16之间且不包含非法字符*#@"></el-input>
        </el-form-item>
        <el-form-item label="密码">
          <el-input v-model="form.password" placeholder="长度在6-16之间且必须包含数字和字母"></el-input>
        </el-form-item>
        <div class="linkto">
          <a href="">忘记密码</a>
          <a href="">立即注册</a>
        </div>
        <el-form-item>
          <button @click="onSubmit">立即登录</button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    const validateNumber = (rule, value, callback) => {
      var reg = /^[0-9a-zA-Z]{6,16}$/; // 账号长度必须在5-16之间，且不能包含非法字符*#@
      if (value === '' || value === undefined) {
        callback(new Error('请输入用户名'))
      } else if (value.length < 6 || value.length > 18) {
        callback(new Error('用户名长度必须在6-16之间'))
      } else if (value.indexOf('*') > 0 || value.indexOf('#') > 0 || value.indexOf('@') > 0) {
        callback(new Error('用户名不能含有非法字符*#@'))
      } else {
        if (reg.test(value)) {
          callback()
        }
      }
    }
    const validatePass = (rule, value, callback) => {
      var reg = /^(?![0-9]+$)(?![a-zA-Z]+$)[0-9a-zA-Z]{6,}$/ // 密码长度必须在6-16之间，且必须包含数字和字母
      if (value === '' || value === undefined) {
        callback(new Error('请输入密码'))
      } else if (value.length < 6 || value.length > 18) {
        callback(new Error('密码长度必须在6-16之间'))
      } else if (/^[a-z]+$/.test(value) || /^[0-9]+$/.test(value)) {
        callback(new Error('密码必须同时包含数字和字母'))
      } else {
        if (reg.test(value)) {
          callback()
        }
      }
    }
    return {
      form: {
        username: '',
        password: ''
      },
      rules: {
        username: [{ required: true, validator: validateNumber, trigger: 'blur' }],
        password: [{ required: true, validator: validatePass, trigger: 'blur' }]
      }
    }
  },
  methods: {
    onSubmit() {
      axios.get('sub/userInfo/login?username=' + this.form.username + '&password=' + this.form.password).then((res) => {
        console.log('login',res)
        if (res.data.code === 200) {
          this.$message({
            type: 'success',
            message: res.data.msg
          })
          this.$router.push({path: '/home'})
        }
      })
    }
  }
}
</script>

<style lang="scss" scoped>
#login {
    width: 100%;
    height: 100vh;
    background: url('../../assets/images/login/login.jpg') no-repeat;
    background-size: cover;
}
.reg_container {
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
}
.el-form {
    width: 380px;
    height:280px;
    margin-top: 100px;
    box-shadow: 0 2px 15px rgba(0,0,0,.15);
    padding: 50px;
    background: #fff;
    h1 {
        text-align: center;
        font-size: 30px;
        font-weight: bold;
        margin-bottom: 30px;
    }
    .linkto {
        display: flex;
        margin-left: 60px;
        justify-content: space-between;
        cursor: pointer;
        a {
          color: #000;  
        }
    }
}
button {
    width: 100%;
    padding: 10px;
    margin-top: 30px;
    cursor: pointer;
    background: #FF6A00;
    border: none;
    font-size: 16px;
}

</style>