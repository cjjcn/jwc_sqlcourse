<template>
  <el-container class="home_container">
    <!-- 头部区域 -->
    <el-header>
      <div>
        <img src="../../assets/logo.png" alt="" />
        <span>东北林业大学教务管理系统-管理员端</span>
      </div>
      <el-button type="info" @click="logout">退出</el-button>
    </el-header>
    <!-- 主体区域 -->
    <el-container>
      <!-- 侧边栏 -->
      <el-aside :width="isCollapse ? '64px' : '200px'">
        <div class="toggle-button" @click="toggleCollapse">|||</div>
        <el-menu
          background-color="#0b5404"
          text-color="#fff"
          unique-opened
          :collapse="isCollapse"
          :collapse-transition="false"
          router
          :default-active="activePath"
        >
          <!-- 一级菜单 -->
          <el-submenu
            :index="item.id + ''"
            v-for="item in menuList"
            :key="item.id"
          >
            <!-- 一级菜单模板 -->
            <template slot="title">
              <!-- 图标 -->
              <i :class="iconsObj[item.id]"></i>
              <!-- 文本 -->
              <span>{{ item.authName }}</span>
            </template>

            <!-- 二级菜单 -->
            <el-menu-item
              v-for="subItem in item.children"
              :key="subItem.id"
              :index="'/admin/' + subItem.path"
              @click="saveNavState('/admin/' + subItem.path)"
            >
              <template slot="title">
                <i class="el-icon-menu"></i>
                <span>{{ subItem.authName }}</span>
              </template>
            </el-menu-item>
          </el-submenu>
        </el-menu>
      </el-aside>
      <!-- 右侧主体 -->
      <el-main>
        <!-- 路由占位符 -->
        <router-view></router-view>
      </el-main>
    </el-container>
  </el-container>
</template>


<script>
export default {
  data() {
    return {
      // 左侧菜单数据
      menuList: [
        {
          id: 1,
          authName: '用户管理',
          path: null,
          children: [
            {
              id: 1,
              authName: '管理员',
              path: 'admins/',
              children: [],
            },
            {
              id: 2,
              authName: '学生',
              path: 'students/',
              children: [],
            },
            {
              id: 3,
              authName: '教师',
              path: 'teachers/',
              children: [],
            },
          ],
        },
        {
          id: 2,
          authName: '信息管理',
          path: null,
          children: [
            {
              id: 1,
              authName: '院系列表',
              path: 'colleges/',
              children: [],
            },
            {
              id: 2,
              authName: '课程列表',
              path: 'courses/',
              children: [],
            },
            {
              id: 3,
              authName: '开课列表',
              path: 'opens/',
              children: [],
            },
          ],
        },
        {
          id: 3,
          authName: '教务管理',
          path: null,
          children: [
            {
              id: 0,
              authName: '添加选课',
              path: 'addSelection/',
              children: [],
            },
            {
              id: 1,
              authName: '选课管理',
              path: 'selections/',
              children: [],
            },
            {
              id: 2,
              authName: '成绩管理',
              path: 'scores/',
              children: [],
            },
            {
              id: 3,
              authName: '成绩分析',
              path: 'scoresAnalysis/',
              children: [],
            },
          ],
        },
      ],
      // 菜单图标
      iconsObj: {
        1: 'el-icon-s-custom',
        2: 'el-icon-s-promotion',
        3: 'el-icon-s-goods',
        4: 'el-icon-s-order',
        5: 'el-icon-s-data',
      },
      // 是否折叠导航菜单栏
      isCollapse: false,
      // 被激活的链接地址
      activePath: '',
    }
  },
  created() {
    // this.getMenuList()
    // 获取左侧链接的激活状态
    this.activePath = window.sessionStorage.getItem('activePath')
  },
  methods: {
    // 退出登录
    logout() {
      window.sessionStorage.clear()
      this.$router.push('/login')
    },
    // 菜单折叠与展开
    toggleCollapse() {
      this.isCollapse = !this.isCollapse
    },
    // 保存链接的激活状态
    saveNavState(activePath) {
      window.sessionStorage.setItem('activePath', activePath)
      this.activePath = activePath
    },
  },
}
</script>


<style lang="less" scoped>
.el-header {
  background-color: #0b5404;
  display: flex;
  justify-content: space-between;
  padding-left: 0;
  align-items: center;
  color: #eceff1;
  font-size: 20px;
  > div {
    display: flex;
    align-items: center;
    span {
      margin-left: 15px;
    }
    img {
      height: 50px;
      width: 50px;
    }
  }
}
.el-aside {
  background-color: #0b5404;
  .el-menu {
    border-right: none;
  }
}
.el-main {
  background-color: #eceff1;
}
.home_container {
  height: 100%;
}
.toggle-button {
  background-color: #0b5404;
  font-size: 10px;
  line-height: 24px;
  color: #fff;
  text-align: center;
  letter-spacing: 0.2em;
}
</style>