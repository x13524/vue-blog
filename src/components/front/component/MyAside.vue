<template>
  <div>
    <H1 style="text-align: center">个人博客站</H1>
    <div class="avatar-box">
      <el-avatar class="avatar-image" :src="circleUrl"></el-avatar>
      <p class="avatar-name">一叶知秋</p>
    </div>
    <el-menu
      router
      default-active="home"
      class="el-menu-vertical-demo"
      @open="handleOpen"
      @close="handleClose"
    >
    <!--  <el-menu-item index="/home">
        <i class="el-icon-s-home"></i>
        <span slot="title">个人首页</span>
      </el-menu-item>-->
      <el-menu-item index="/articles">
        <i class="el-icon-document-copy"></i>
        <span slot="title">个人博客</span>
      </el-menu-item>
      <el-menu-item index="/admin/posts">
        <i class="el-icon-s-management"></i>
        <span slot="title">博客管理</span>
      </el-menu-item>
      <!--<el-submenu index="1">
        <template slot="title">
          <i class="el-icon-collection-tag"></i>
          <span>标签分类</span>
        </template>
        <el-menu-item-group>
          <el-menu-item index="articles">默认分类</el-menu-item>
          <el-menu-item index="1-2">选项2</el-menu-item>
          <el-menu-item index="1-3">选项3</el-menu-item>
        </el-menu-item-group>
      </el-submenu>-->
    </el-menu>
  </div>
  <!--  <div class="flexDiv">
      <nav>
        <ul class="catalog">
          <router-link to="/home" tag="li">首页</router-link>
          <router-link to="/articles" tag="li">博客</router-link>
          <router-link to="/contact" tag="li">联系站长</router-link>
          <router-link to="/about" tag="li">关于我</router-link>
        </ul>
      </nav>
    </div>-->
</template>

<script>
export default {
    data () {
        return {
            circleUrl: 'https://cube.elemecdn.com/3/7c/3ea6beec64369c2642b92c6726f1epng.png'
        }
    },
    methods: {
        handleOpen (key, keyPath) {
            console.log(key, keyPath)
        },
        handleClose (key, keyPath) {
            console.log(key, keyPath)
        }
    }
}
</script>

<style lang="scss" rel="stylesheet/scss" scoped>
.avatar-box {
  text-align: center;
  box-sizing: border-box;
  padding: 15px;
}

.avatar-image {
  width: 96px;
  height: 96px;
}

.avatar-name {
  font-size: 20px;
}
</style>
