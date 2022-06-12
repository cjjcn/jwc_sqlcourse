<template>
  <div>
    <div class="main"><h1>管理员（工号：{{name}}）你好，欢迎登录东北林业大学教务系统！</h1></div>
  </div>
</template>
<script>
export default {
  data(){
    return  {
      name:sessionStorage.getItem('user')
    }
  }
}
</script>
</script>
<style lang="less" scoped>
.main{
  display: flex;
  justify-content: center;
  align-content: center;
}
</style>