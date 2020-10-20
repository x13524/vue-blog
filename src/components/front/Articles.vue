<template>
  <div class="articleContent">
    <div id="articles">
      <div class="tags animated fadeIn">
        <div class="tagFlex">
          <button
            v-for="(tag, index) in allTags"
            :key="index"
            v-bind:class="{activeBtn: selectIndex === index}"
            v-on:click="switchTag({value: tag, currentPage: 1}, index, tag)"
          >
            <span>{{ tag }}</span>
          </button>
        </div>
      </div>

      <el-card v-for="(article, index) in reducedArticles" :key="article.id" id="article"
               class="article-card-box animated fadeIn">
        <router-link
          :to="{name: 'article', params: {id: article.aid, index: index, page: currentPage}, hash: '#article'}"
          exact>
          <h2> {{ article.title }}</h2>
        </router-link>
        <time><i class="iconfont icon-shijian"></i>{{ article.date | toDate }}</time>
        <span class="articleTag"><i class="iconfont icon-label"></i>{{ article.tags | toTag }}</span>
        <span class="commentNumber"><i class="iconfont icon-huifu"></i>{{ article.comment_n }}</span>
        <p>{{ article.content }}</p>
      </el-card>

      <!--TODO: 总数还么获取正确, 需要调整-->
      <div style="text-align: center;margin-bottom: 30px">
        <el-pagination
          @current-change="handleCurrentChange"
          background
          hide-on-single-page
          :current-page="currentPage"
          layout="total, prev, pager, next, jumper"
          :total="50"
        >
        </el-pagination>
      </div>
    </div>
    <spinner v-show="loadMore" class="spinner"></spinner>
  </div>
</template>

<script>
  import {mapMutations, mapActions, mapGetters, mapState} from 'vuex'
  import spinner from '../share/spinner'

  export default {
      data () {
          return {
              selectIndex: 0,
              currentPage: 1
          }
      },
      created () {
          this.getAllArticles({page: 1, limit: 10})
          this.getAllTags()
      },
      computed: {
          ...mapGetters(['reducedArticles', 'allTags']),
          ...mapState(['curTag', 'loadMore', 'moreArticle', 'isLoading', 'noMore', 'total'])
      },
      // mounted () {
      //     window.addEventListener('scroll', this.handleScroll)
      // },
      // beforeRouteLeave (to, from, next) {
      //     window.removeEventListener('scroll', this.handleScroll)
      //     next()
      // },
      methods: {
          ...mapMutations(['set_headline', 'set_curtag', 'moreArticle_toggle']),
          ...mapActions(['getAllArticles', 'getAllTags', 'searchArticles']),
          switchTag (payload, index, tag) {
              this.getAllArticles(payload)
              this.selectIndex = index
              this.set_curtag(tag)
          },
          handleCurrentChange (val) {
              console.log(`当前页: ${val}`)
              this.currentPage = val
              this.getAllArticles({value: this.curTag, limit: 10, page: val})
          }
      },
      components: {
          spinner
      }
  }

</script>

<style lang="scss" rel="stylesheet/scss" scoped>
  .articleContent {
    #articles {
      padding: 1.5rem 4rem 0;

      .tags {
        .tagFlex {
          display: flex;
          flex-wrap: wrap;
          justify-content: space-around;

          .activeBtn {
            background: #ffc520;
            transition: 1s;
          }

          button {
            transition: 1s;
            padding-left: 1rem;
            padding-right: 0.2rem;
            text-align: center;
            background: rgb(129, 216, 208);
            color: #00193a;
            margin: 0 1.25rem 1.25rem 0;
          }
        }
      }

      .article-card-box {
        width: 100%;
        padding: 30px;
        border-radius: 2px;
        margin-bottom: 20px;
        box-sizing: border-box;

        h2 {
          margin-bottom: 1.25rem;
          color: #58666e;
        }

        time {
          margin-top: 0.625rem;
          margin-right: 0.625rem;
        }

        p {
          margin-top: 1.875rem;
          -webkit-box-orient: vertical;
          height: 66px;
          line-height: 22px;
          overflow: hidden;
          text-overflow: ellipsis;
          display: -webkit-box;
          overflow: hidden; /*超出隐藏*/
          text-overflow: ellipsis; /*文本溢出时显示省略标记*/
          -webkit-line-clamp: 3; /*文本占的行数,如果要设置2行加...则设置为2*/
          -webkit-box-orient: vertical; /*子代元素垂直显示*/

        }

        .articleTag {
          margin-bottom: 1.875rem;
          margin-right: 0.625rem;
        }

        .commentNumber {

          i {
            font-size: 1.125rem;
            margin-right: 0.3125rem;
          }
        }

        i.icon-label, i.icon-shijian {
          font-size: 1.25rem;
          margin-right: 0.3125rem;
        }
      }


      p.noMore {
        width: 100%;
        height: 1.5rem;
        line-height: 1.5rem;
        margin-top: 1.875rem;
        margin-bottom: 1.875rem;
        text-align: center;
      }
    }
  }

</style>
