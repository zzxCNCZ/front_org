<template>
  <el-dialog
    :title="!dataForm.id ? '新增' : '修改'"
    :close-on-click-modal="false"
    :visible.sync="visible">
    <el-form :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmit()" label-width="80px">
    <el-form-item label="" prop="pxyj">
      <el-input v-model="dataForm.pxyj" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="jgjc">
      <el-input v-model="dataForm.jgjc" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="jgmc">
      <el-input v-model="dataForm.jgmc" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="jgbm">
      <el-input v-model="dataForm.jgbm" placeholder=""></el-input>
    </el-form-item>
    </el-form>
    <span slot="footer" class="dialog-footer">
      <el-button @click="visible = false">取消</el-button>
      <el-button type="primary" @click="dataFormSubmit()">确定</el-button>
    </span>
  </el-dialog>
</template>

<script>
export default {
  data () {
    return {
      visible: false,
      dataForm: {
        istest: 0,
        pxyj: '',
        jgjc: '',
        jgmc: '',
        jgbm: ''
      },
      dataRule: {
        pxyj: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        jgjc: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        jgmc: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        jgbm: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    init (id) {
      this.dataForm.istest = id || 0
      this.visible = true
      this.$nextTick(() => {
        this.$refs['dataForm'].resetFields()
        if (this.dataForm.istest) {
          this.$http({
            url: this.$http.adornUrl(`/user/vwtpdeparts/info/${this.dataForm.istest}`),
            method: 'get',
            params: this.$http.adornParams()
          }).then(({data}) => {
            if (data && data.code === 0) {
              this.dataForm.pxyj = data.vwTpDeparts.pxyj
              this.dataForm.jgjc = data.vwTpDeparts.jgjc
              this.dataForm.jgmc = data.vwTpDeparts.jgmc
              this.dataForm.jgbm = data.vwTpDeparts.jgbm
            }
          })
        }
      })
    },
    // 表单提交
    dataFormSubmit () {
      this.$refs['dataForm'].validate((valid) => {
        if (valid) {
          this.$http({
            url: this.$http.adornUrl(`/user/vwtpdeparts/${!this.dataForm.istest ? 'save' : 'update'}`),
            method: 'post',
            data: this.$http.adornData({
              'istest': this.dataForm.istest || undefined,
              'pxyj': this.dataForm.pxyj,
              'jgjc': this.dataForm.jgjc,
              'jgmc': this.dataForm.jgmc,
              'jgbm': this.dataForm.jgbm
            })
          }).then(({data}) => {
            if (data && data.code === 0) {
              this.$message({
                message: '操作成功',
                type: 'success',
                duration: 1500,
                onClose: () => {
                  this.visible = false
                  this.$emit('refreshDataList')
                }
              })
            } else {
              this.$message.error(data.msg)
            }
          })
        }
      })
    }
  }
}
</script>
