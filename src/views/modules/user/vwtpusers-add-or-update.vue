<template>
  <el-dialog
    :title="!dataForm.id ? '新增' : '修改'"
    :close-on-click-modal="false"
    :visible.sync="visible">
    <el-form :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmit()" label-width="80px">
    <el-form-item label="" prop="jgbm">
      <el-input v-model="dataForm.jgbm" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="mjxm">
      <el-input v-model="dataForm.mjxm" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="mjjh">
      <el-input v-model="dataForm.mjjh" placeholder=""></el-input>
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
        jgmc: 0,
        jgbm: '',
        mjxm: '',
        mjjh: ''
      },
      dataRule: {
        jgbm: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        mjxm: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        mjjh: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    init (id) {
      this.dataForm.jgmc = id || 0
      this.visible = true
      this.$nextTick(() => {
        this.$refs['dataForm'].resetFields()
        if (this.dataForm.jgmc) {
          this.$http({
            url: this.$http.adornUrl(`/user/vwtpusers/info/${this.dataForm.jgmc}`),
            method: 'get',
            params: this.$http.adornParams()
          }).then(({data}) => {
            if (data && data.code === 0) {
              this.dataForm.jgbm = data.vwTpUsers.jgbm
              this.dataForm.mjxm = data.vwTpUsers.mjxm
              this.dataForm.mjjh = data.vwTpUsers.mjjh
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
            url: this.$http.adornUrl(`/user/vwtpusers/${!this.dataForm.jgmc ? 'save' : 'update'}`),
            method: 'post',
            data: this.$http.adornData({
              'jgmc': this.dataForm.jgmc || undefined,
              'jgbm': this.dataForm.jgbm,
              'mjxm': this.dataForm.mjxm,
              'mjjh': this.dataForm.mjjh
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
