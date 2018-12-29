<template lang="html">
  <el-row style="text-align: center" >
    <vue-ueditor-wrap v-model="msg"></vue-ueditor-wrap>
  </el-row>
</template>

<style scoped>
</style>

<script>
import VueUeditorWrap from 'vue-ueditor-wrap'
import axios from 'axios'
export default {
  data: function () {
    return {
      msg: '<h2>Vue + UEditor + v-model双向绑定</h2>'
    }
  },
  components: {
    VueUeditorWrap
  },
  mounted () {
    // this.onload()
  },
  methods: {
    onload () {
      let that = this
      axios.get('http://www.grandlynn.com/apis/user/newsinfo/getNewsById?id=20')
        .then(function (data) {
          console.log(data.data)
          that.contentHtml = data.data.newsInfo.content
        })
    },
  }
}

</script>
