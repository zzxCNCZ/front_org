<template>
  <el-dialog
    :title="!dataForm.id ? '新增' : '修改'"
    :close-on-click-modal="false"
    :visible.sync="visible">
    <el-form :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmit()" label-width="80px">
    <el-form-item label="警员编码" prop="code">
      <el-input v-model="dataForm.code" placeholder="警员编码"></el-input>
    </el-form-item>
    <el-form-item label="用户名" prop="username">
      <el-input v-model="dataForm.username" placeholder="用户名"></el-input>
    </el-form-item>
    <el-form-item label="密码" prop="password">
      <el-input v-model="dataForm.password" placeholder="密码"></el-input>
    </el-form-item>
    <el-form-item label="警员姓名" prop="trueName">
      <el-input v-model="dataForm.trueName" placeholder="警员姓名"></el-input>
    </el-form-item>
    <el-form-item label="部门编码" prop="deptCode">
      <el-input v-model="dataForm.deptCode" placeholder="部门编码"></el-input>
    </el-form-item>
    <el-form-item label="职位" prop="position">
      <el-input v-model="dataForm.position" placeholder="职位"></el-input>
    </el-form-item>
    <el-form-item label="手机号码" prop="mobilePhone">
      <el-input v-model="dataForm.mobilePhone" placeholder="手机号码"></el-input>
    </el-form-item>
    <el-form-item label="办公室电话号码" prop="officePhone">
      <el-input v-model="dataForm.officePhone" placeholder="办公室电话号码"></el-input>
    </el-form-item>
    <el-form-item label="email" prop="email">
      <el-input v-model="dataForm.email" placeholder="email"></el-input>
    </el-form-item>
    <el-form-item label="更新时间" prop="updateTime">
      <el-input v-model="dataForm.updateTime" placeholder="更新时间"></el-input>
    </el-form-item>
    <el-form-item label="密码更新时间" prop="passwordUpdateTime">
      <el-input v-model="dataForm.passwordUpdateTime" placeholder="密码更新时间"></el-input>
    </el-form-item>
    <el-form-item label="删除时间" prop="delTime">
      <el-input v-model="dataForm.delTime" placeholder="删除时间"></el-input>
    </el-form-item>
    <el-form-item label="用户状态" prop="status">
      <el-input v-model="dataForm.status" placeholder="用户状态"></el-input>
    </el-form-item>
    <el-form-item label="备注" prop="note">
      <el-input v-model="dataForm.note" placeholder="备注"></el-input>
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
        id: 0,
        code: '',
        username: '',
        password: '',
        trueName: '',
        deptCode: '',
        position: '',
        mobilePhone: '',
        officePhone: '',
        email: '',
        updateTime: '',
        passwordUpdateTime: '',
        delTime: '',
        status: '',
        note: ''
      },
      dataRule: {
        code: [
          { required: true, message: '警员编码不能为空', trigger: 'blur' }
        ],
        username: [
          { required: true, message: '用户名不能为空', trigger: 'blur' }
        ],
        password: [
          { required: true, message: '密码不能为空', trigger: 'blur' }
        ],
        trueName: [
          { required: true, message: '警员姓名不能为空', trigger: 'blur' }
        ],
        deptCode: [
          { required: true, message: '部门编码不能为空', trigger: 'blur' }
        ],
        position: [
          { required: true, message: '职位不能为空', trigger: 'blur' }
        ],
        mobilePhone: [
          { required: true, message: '手机号码不能为空', trigger: 'blur' }
        ],
        officePhone: [
          { required: true, message: '办公室电话号码不能为空', trigger: 'blur' }
        ],
        email: [
          { required: true, message: 'email不能为空', trigger: 'blur' }
        ],
        updateTime: [
          { required: true, message: '更新时间不能为空', trigger: 'blur' }
        ],
        passwordUpdateTime: [
          { required: true, message: '密码更新时间不能为空', trigger: 'blur' }
        ],
        delTime: [
          { required: true, message: '删除时间不能为空', trigger: 'blur' }
        ],
        status: [
          { required: true, message: '用户状态不能为空', trigger: 'blur' }
        ],
        note: [
          { required: true, message: '备注不能为空', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    init (id) {
      this.dataForm.id = id || 0
      this.visible = true
      this.$nextTick(() => {
        this.$refs['dataForm'].resetFields()
        if (this.dataForm.id) {
          this.$http({
            url: this.$http.adornUrl(`/user/ctuser/info/${this.dataForm.id}`),
            method: 'get',
            params: this.$http.adornParams()
          }).then(({data}) => {
            if (data && data.code === 0) {
              debugger
              this.dataForm.code = data.ctUser.code
              this.dataForm.username = data.ctUser.username
              this.dataForm.password = data.ctUser.password
              this.dataForm.trueName = data.ctUser.trueName
              this.dataForm.deptCode = data.ctUser.deptCode
              this.dataForm.position = data.ctUser.position
              this.dataForm.mobilePhone = data.ctUser.mobilePhone
              this.dataForm.officePhone = data.ctUser.officePhone
              this.dataForm.email = data.ctUser.email
              this.dataForm.updateTime = data.ctUser.updateTime
              this.dataForm.passwordUpdateTime = data.ctUser.passwordUpdateTime
              this.dataForm.delTime = data.ctUser.delTime
              this.dataForm.status = data.ctUser.status
              this.dataForm.note = data.ctUser.note
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
            url: this.$http.adornUrl(`/user/ctuser/${!this.dataForm.id ? 'save' : 'update'}`),
            method: 'post',
            data: this.$http.adornData({
              'id': this.dataForm.id || undefined,
              'code': this.dataForm.code,
              'username': this.dataForm.username,
              'password': this.dataForm.password,
              'trueName': this.dataForm.trueName,
              'deptCode': this.dataForm.deptCode,
              'position': this.dataForm.position,
              'mobilePhone': this.dataForm.mobilePhone,
              'officePhone': this.dataForm.officePhone,
              'email': this.dataForm.email,
              'updateTime': this.dataForm.updateTime,
              'passwordUpdateTime': this.dataForm.passwordUpdateTime,
              'delTime': this.dataForm.delTime,
              'status': this.dataForm.status,
              'note': this.dataForm.note
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
