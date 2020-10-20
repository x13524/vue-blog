<template>
  <el-container id="wrapper">
    <el-aside width="200px">
      <my-aside>12312321</my-aside>
    </el-aside>
    <el-container>
      <el-header>
        <my-header></my-header>
      </el-header>
      <el-main>
        <router-view class="content" v-show="!isLoading"></router-view>
        <spinner v-show="isLoading"></spinner>
        <my-footer></my-footer>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
import MyHeader from './component/MyHeader'
import MyFooter from './component/MyFooter'
import MyAside from './component/MyAside'
import spinner from '../share/spinner'
import {mapState} from 'vuex'

export default {
    data () {
        return {
            show: false
        }
    },
    mounted () {
    // window.addEventListener('scroll', this.handleScroll)
    },
    computed: {
        ...mapState(['isLoading'])
    },
    methods: {
    // handleScroll () {
    //     this.show = window.scrollY > 400
    // }
    },
    components: {
        MyHeader,
        MyAside,
        MyFooter,
        spinner
    }
}
</script>

<style lang="scss" rel="stylesheet/scss" scoped>
@import '../../assets/css/icon.scss';

#wrapper {
  margin: 0 auto;
  height: 100%;
  max-width: 1200px;
  box-shadow: 0 0 30px rgba(0, 0, 0, .3);
}

.icon-huojian {
  font-size: 2.5rem;
  color: #C0CCDA;
  position: fixed;
  bottom: 1.25rem;
  right: 2.5rem;
  cursor: pointer;
  transition: 1s;

  &:hover {
    bottom: 1.875rem;
    color: #00ff7f;
    transition: 1s;
  }
}

.totop {
  bottom: 31.25rem;
  transition: 1s;
}

@media screen and (max-width: 440px) {
  .icon-huojian {
    right: 0.5rem;
  }
}


/*--- 样式调整 ----*/
.el-header, .el-footer {
  height: 60px;
  padding: 0;
}

.el-aside {
  //background-color: #D3DCE6;
  //color: #333;
  //text-align: center;
  padding: 0;
  background-color: #f0f3f4;
}

.el-main {
  padding: 0;
  color: #58666e;
}

/*控制整个滚动条*/
::-webkit-scrollbar {
  background-color: lightgray;
  width: 10px;
  height: 10px;
  background-clip: padding-box;
}

/*滚动条两端方向按钮*/
::-webkit-scrollbar-button {
  display: none;
}

/*滚动条中间滑动部分*/
::-webkit-scrollbar-thumb {
  background-color: #1199c4;
  border-radius: 5px;
}

/*滚动条右下角区域*/
::-webkit-scrollbar-corner {
  display: none;
}
</style>
