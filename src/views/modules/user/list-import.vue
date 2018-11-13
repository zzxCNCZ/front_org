<template>
  <el-dialog
    :title="'导入'"
    :close-on-click-modal="false"
    :visible.sync="visible">
    <el-upload
      class="upload-demo"
      ref="upload"
      :action="uploadUrl()"
      :headers="headers()"
      accept=".xls,.xlsx"
      :on-preview="handlePreview"
      :on-remove="handleRemove"
      :file-list="fileList"
      :auto-upload="false">
      <el-button slot="trigger" size="small" type="primary">选取文件</el-button>
      <el-button style="margin-left: 10px;" size="small" type="success" @click="submitUpload">上传到服务器</el-button>
      <div slot="tip" class="el-upload__tip">只能上传xls/xlsx文件，且不超过2M</div>
    </el-upload>
  </el-dialog>
</template>

<script>
import Vue from 'vue'
export default {
  name: 'list-import',
  data () {
    return {
      fileList: [],
      visible: false
    }
  },
  methods: {
    headers () {
      return {
        'token': Vue.cookie.get('token')
      }
    },
    uploadUrl () {
      return this.$http.adornUrl(`/user/ctuser/import`)
    },
    init () {
      this.visible = true
    },
    submitUpload () {
      this.$refs.upload.submit()
    },
    handleRemove (file, fileList) {
      console.log(file, fileList)
    },
    handlePreview (file) {
      console.log(file)
    }
  }
}
</script>

<style scoped>

</style>
