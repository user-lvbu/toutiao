<template>
  <div class="home-container">
    <van-nav-bar title="头条" fixed placeholder/>

    <van-list
  v-model="loading"
  :finished="finished"
  finished-text="没有更多了"
  @load="onLoad"
>
    <ArticleInfo v-for="item in artList" :key='item.id'
    :title="item.title"
    :author="item.title"
    :cmt-count="item.comm_count"
    :time="item.pubdate"
    :cover="item.cover"
    ></ArticleInfo>
  </van-list>
  </div>
</template>

<script>
// 按需导入API接口
import { getArticleListAPI } from '@/api/articleAPI.js'
// 按需导入组件
import ArticleInfo from '@/components/Article/AtricleInfo.vue'

export default {
  name: 'MyHome',
  data () {
    return {
      page: 1,
      limit: 10,
      artList: [],
      loading: true,
      finished: false,
      isLoading: false
    }
  },
  created () {
    this.initArticleLIst()
  },
  methods: {
    // 封装获取文章数据的方法
    async initArticleLIst () {
      const { data: res } = await getArticleListAPI(this.page, this.limit)
      this.artList = res
    },
    onLoad () {
      console.log('触发了 load 事件')
      this.page++
      this.initArticleLIst()
    }
  },
  components: {
    ArticleInfo
  }
}
</script>

<style lang="less" scoped>
/deep/ .van-nav-bar {
  background-color: red;
}
/deep/ .van-nav-bar__title{
  color:white
}
</style>
