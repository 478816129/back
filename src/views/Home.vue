<template>
  <el-container  class="home">
    <el-header>
        <div>
         <img src="../assets/timg.jpg" alt="">
        <span>电商后台管理系统</span>
        </div>
        
      
      <el-button type="info" @click="logout">退出</el-button>
      </el-header>
    <!-- 页面主体 -->
    <el-container>
      <el-aside width="200px">Aside</el-aside>
      <el-main>Main</el-main>
    </el-container>
  </el-container>
</template>

<script>
export default {
  methods: {
    logout() {
      window.sessionStorage.clear();
      this.$router.push("/login");
    },
  },
};
</script>
<style scoped>
.home{
  height: 100%;
}
.el-header{
  background-color: #373d41;
  display: flex;
  justify-content: space-between;
  padding-left:0 ;
  align-items: center;
  color: white;
}
.el-header>div{
  display: flex;
  align-items: center;
}
.el-header>div>span{
  margin-left: 10px;
  font-size: 22px;
  font-family: STHupo;
}
/* .el-button{
  justify-content: right;
} */

img{
  
  height: 60px;
  width: 60px;
  /* width: 100%;height: 100%; */
}
.el-header>span{
  color: #eaedf1;
}
.el-aside{
 background-color: #333744;
}
.el-main{
 background-color: #eaedf1;
}
</style>
