<template>
  <div class="login" @keyup.enter="submitForm">
    <div class="topbar">
      <div class="container ">
        <span>网站管理后台</span><span class="regist">注册</span>
      </div>
    </div>
    <div class="form container">
      <div class="welcome">
        <p>欢迎来到</p>
        <p>xxx后台</p>
        <p>管理系统</p>
        <p class="introduce">介绍介绍介绍介绍</p>
      </div>
      <div id="box">
        <div class="title">
          <p>欢迎登录</p>
        </div>
        <el-form
          :model="loginForm"
          :rules="rules"
          ref="loginFormId"
          label-width="70px"
          class="demo-ruleForm"
        >
          <p class="user">用户名</p>
          <el-form-item prop="username">
            <el-input
              clearable
              type="text"
              v-model="loginForm.username"
              placeholder="用户名"
              autocomplete="off"
              prefix-icon="el-icon-s-custom"
            ></el-input>
          </el-form-item>
          <p class="password">密码</p>
          <el-form-item prop="password">
            <el-input
              prefix-icon="el-icon-key"
              placeholder="密码"
              type="password"
              v-model="loginForm.password"
              autocomplete="off"
              show-password
            ></el-input>
          </el-form-item>
          <el-form-item class="bottom">
            <el-checkbox v-model="loginForm.checked">下次自动登录</el-checkbox>
            <a class="right">忘记密码?</a>
          </el-form-item>

          <el-form-item>
            <input
              type="button"
              name=""
              id="btn"
              value="登录"
              @click="submitForm()"
            />
          </el-form-item>
        </el-form>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";

export default {
  data() {
    return {
      loginForm: {
        username: "",
        password: "",
        checked: true,
      },
      rules: {
        username: [
          {
            min: 3,
            max: 10,
            message: "长度在 3 到 10 个字符",
            trigger: "blur",
          },
          { required: true, message: "请输入用户名", trigger: "blur" },
        ],
        password: [{ required: true, message: "请输入密码", trigger: "blur" }],
      },
    };
  },
  methods: {
    submitForm() {
      var a = this;
      this.$refs.loginFormId.validate((valid) => {
        if (valid) {
          axios
            .post("http://127.0.0.1:3000/login", {
              username: a.loginForm.username,
              password: a.loginForm.password,
            })
            .then(function({ data }) {
              if (data.success) {
                //  sessionStorage.setItem('token',JSON.stringify({ tokenId:data.tokenId }))
                // a.$store.state.tokenId=data.tokenId;
                a.$message({
                  showClose: true,
                  message: data.message,
                  type: "success",
                  duration: 1000,
                  onClose: () => {
                    a.$router.replace("/home/homemange");
                  },
                });
              } else {
                a.$message({
                  showClose: true,
                  message: data.message,
                  type: "error",
                  duration: 1000,
                });
              }
            })
            .catch(function(error) {
              console.log(error);
            });
        } else {
          this.$message({
            showClose: true,
            message: "错了哦，这是一条错误消息",
            type: "error",
          });
        }
      });
    },
  },
};
</script>
<style lang="less" scoped>
.login {
  height: 100%;
  opacity: 0.8;
  background: skyblue;
  font-family: "Source Han Serif CN";
  .container {
    width: 1200px;
    margin: 0 auto;
  }
  .topbar {
    font-size: 24px;
    height: 80px;
    background: #333;
    color: #fff;
    line-height: 80px;
    div {
      display: flex;
      justify-content: space-between;
      .regist{
        font-size: 20px;
      }
    }
  }
  #box {
    padding-right: 50px;
    padding-top: 70px;
    padding-bottom: 28px;
    width: 490px;
    background: white;
    font-family: "Source Han Serif CN";
    margin: 0;
    p {
      font-size: 24px;
      text-indent: 70px;
    }
    .title {
      margin-bottom: 50px;
    }
    .password,
    .user {
      margin-top: 30px;
      font-size: 14px;
      font-family: "Source Han Serif CN";
      margin-bottom: 10px;
    }
    .el-form {
      width: 490px;
    }
  }
  .form {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 20px;
    .welcome {
      font-size: 57px;
      color: #fff;
      .introduce {
        font-size: 16px;
        margin-top: 20px;
      }
    }
  }
  .clearfix:before,
  .clearfix:after {
    display: table;
    content: "";
  }
  .clearfix:after {
    clear: both;
  }
  .bottom .right {
    float: right;
    cursor: pointer;
  }
  #btn {
    width: 420px;
    border: 0;
    height: 46px;
    background: orangered;
    color: white;
    margin-top: 60px;
    border-radius: 10px;
    outline: none;
  }
  #btn:hover {
    background: rgba(247, 73, 10, 0.8);
    cursor: pointer;
  }
//   .el-form-item__label{
//  vertical-align: left;
//   }
}
</style>
