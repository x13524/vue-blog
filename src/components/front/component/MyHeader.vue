<template>
  <div id="nav">
    <div class="flexDiv">
      <div class="search">
        <el-input placeholder="请输入内容" v-model="text" @keydown.enter="search" >
          <el-button slot="append" icon="el-icon-search" @click="search"></el-button>
        </el-input>
      </div>
      <el-menu default-active="articles" class="el-menu-demo" router mode="horizontal" @select="handleSelect">
        <el-menu-item index="articles">所有博客</el-menu-item>
        <el-menu-item index="contact">联系站长</el-menu-item>
        <el-menu-item index="about">关于站长</el-menu-item>
        <el-menu-item index="login">注册/登录</el-menu-item>
      </el-menu>
    </div>
  <!--  <div class="container">
      <div :class="headline.animation" id="title">
        {{ headline.content }}
      </div>
    </div>-->
  </div>
</template>

<script>
import {mapState, mapActions} from 'vuex'

export default {
    data () {
        return {
            text: '',
            activeIndex: '1'
        }
    },
    computed: mapState(['headline']),
    methods: {
        ...mapActions(['searchArticles']),
        search () {
            this.$router.push({name: 'SearchResult', params: {text: this.text}, hash: '#search'})
        },
        handleSelect (key, keyPath) {
            console.log(key, keyPath)
        }
    },
    watch: {
        $route () {
            this.text = ''
        }
    }
}
</script>

<style lang="scss" rel="stylesheet/scss" scoped>
#nav {
  position: relative;
  height: 100%;

  .flexDiv {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap-reverse;
    width: 100%;
    height: 100%;

    .search {
      position: relative;
      display: flex;
      align-items: center;
      margin-left: 20px;
    }

    nav {
      width: 50%;
      height: 3.125rem;

      ul {
        color: white;
        display: flex;
        flex-wrap: nowrap;
        justify-content: space-around;
        list-style: none;
        width: 100%;

        li {
          width: 7rem;
          font-size: 1.125rem;
          text-align: center;
          margin-right: 1.2rem;
          height: 2.9375rem;
          line-height: 3.3125rem;
          cursor: pointer;
          border-bottom: 0.1875rem solid transparent;

          &:hover {
            border-bottom: 0.1875rem solid rgb(129, 216, 208);
            transition: all 0.8s;
          }

          &.router-link-active {
            border-bottom: 0.1875rem solid rgb(129, 216, 208);
          }
        }
      }
    }
  }

  .container {
    width: 100%;
    height: 100%;
  }

  .bgImage {
    display: block;
    width: 100%;
    height: 37.5rem;
    transform: perspective(62.5rem) translateZ(0);
    transition: 8s;

    &:hover {
      transform: perspective(62.5rem) translateZ(6.25rem);
      transition: 8s;
    }
  }

  #title {
    font-family: Georgia, "Microsoft YaHei", "微软雅黑", STXihei, "华文细黑", serif;
    color: #fff;
    text-align: center;
    font-size: 3.125rem;
    width: 31.25rem;
    height: 3.125rem;
    position: absolute;
    top: 50%;
    left: 50%;
    margin-top: -0.625rem;
    margin-left: -15.625rem;
  }
}

@media screen and (max-width: 980px) {
  nav {
    width: 60% !important;
  }
}

@media screen and (max-width: 440px) {
  .container, .bgImage {
    height: 18rem !important;
  }
  #title {
    font-size: 2rem !important;
  }
  nav {
    width: 100% !important;

    ul {
      width: 100% !important;
      padding-left: 0 !important;

      li {
        font-size: 0.9rem !important;
        margin-right: 0 !important;
      }
    }
  }
  .search {
    z-index: 2;
    position: absolute !important;
    top: 3.2rem;
    left: 50%;
    margin-left: -8.125rem !important;
  }
}
</style>
