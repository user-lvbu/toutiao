<template>
  <div>
    <h1>User组件</h1>
  </div>
</template>

<script>
import { getArticleListAPI } from '@/api/articleAPI.js'
export default {
  name: 'MyUser',
  data () {
    return {
      page: 1,
      limit: 5
    }
  },
  methods: {
    async initArticleLIst () {
      const { data: res } = await getArticleListAPI(this.page, this.limit)
      console.log(res)
    }
  },
  created () {
    this.initArticleLIst()
  }
}
</script>

<style lang="less" scoped>

</style>
