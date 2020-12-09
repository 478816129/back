<template>
  <div class="login_container">
    <div class="login_box">
      <div class="avatar_box">
        <img src="../assets/timg.jpg" alt="" />
      </div>
      <!-- 登录表单区 -->
      <el-form
        :model="loginForm"
        :rules="loginRules"
        label-width="0px"
        class="login_form"
        ref="loginclear"
      >
        <el-form-item prop="username">
          <el-input v-model="loginForm.username">
            <i slot="prefix" class="el-input__icon el-icon-user-solid"></i
          ></el-input>
        </el-form-item>
        <el-form-item prop="password">
          <el-input v-model="loginForm.password" type="password">
            <i slot="prefix" class="el-input__icon el-icon-s-goods"></i
          ></el-input>
        </el-form-item>
        <el-form-item class="btn">
          <el-button type="primary" @click="checktrue">登录</el-button>
          <el-button type="info" @click="loginreset">重置</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loginForm: {
        username: "admin",
        password: "123456",
      },
      loginRules: {
        username: [
          { required: true, message: "请输入姓名", trigger: "blur" },
          { min: 3, max: 5, message: "长度在 3 到 5 个字符", trigger: "blur" },
        ],
        password: [
          { required: true, message: "请输入密码", trigger: "blur" },
          { min: 3, max: 8, message: "长度在 3 到 5 个字符", trigger: "blur" },
        ],
      },
    };
  },
  methods: {
    loginreset() {
      this.$refs.loginclear.resetFields();
    },
    checktrue() {
      this.$refs.loginclear.validate(async (valid) => {
        if (!valid) {
          return;
        } else {
          const { data: res } = await this.axios.post("login", this.loginForm);
          
           console.log(res)
          if (res.meta.status !== 200) {
            // console.log(res)
            return this.$message.error("登陆失败");
          } else {
            this.$message.success("登陆成功");
            window.sessionStorage.setItem("token",res.meta.token)
            this.$router.push("/home")
          }
        }
      });
    },
  },
};
</script>
<style scoped>
.login_container {
  background-color: #2b4b6b;
  height: 100%;
}
.login_box {
  width: 450px;
  height: 300px;
  background-color: #fff;
  border-radius: 3px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
.avatar_box {
  height: 130px;
  width: 130px;
  border: 1px solid #eee;
  border-radius: 50%;
  padding: 10px;
  box-shadow: 0 0 10px #ddd;
  position: absolute;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #fff;
}
img {
  width: 100%;
  height: 100%;
  border-radius: 50%;
  background-color: #eee;
}
.btn {
  display: flex;
  justify-content: flex-end;
}
.login_form {
  position: absolute;
  bottom: 0;
  width: 100%;
  padding: 0 20px;
  box-sizing: border-box;
}
</style>