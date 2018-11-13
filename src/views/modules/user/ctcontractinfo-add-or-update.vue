<template>
  <el-dialog
    :title="!dataForm.id ? '新增' : '修改'"
    :close-on-click-modal="false"
    :visible.sync="visible">
    <el-form :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmit()" label-width="80px">
    <el-form-item label="合同名称" prop="conName">
      <el-input v-model="dataForm.conName" placeholder="合同名称"></el-input>
    </el-form-item>
    <el-form-item label="项目编号" prop="proId">
      <el-input v-model="dataForm.proId" placeholder="项目编号"></el-input>
    </el-form-item>
    <el-form-item label="所属区域" prop="area">
      <el-input v-model="dataForm.area" placeholder="所属区域"></el-input>
    </el-form-item>
    <el-form-item label="项目甲方" prop="proFirstParty">
      <el-input v-model="dataForm.proFirstParty" placeholder="项目甲方"></el-input>
    </el-form-item>
    <el-form-item label="最终用户" prop="lastUser">
      <el-input v-model="dataForm.lastUser" placeholder="最终用户"></el-input>
    </el-form-item>
    <el-form-item label="所属产品部" prop="productionDep">
      <el-input v-model="dataForm.productionDep" placeholder="所属产品部"></el-input>
    </el-form-item>
    <el-form-item label="主要功能点" prop="mainFunction">
      <el-input v-model="dataForm.mainFunction" placeholder="主要功能点"></el-input>
    </el-form-item>
    <el-form-item label="合同签订时间" prop="signdate">
      <el-input v-model="dataForm.signdate" placeholder="合同签订时间"></el-input>
    </el-form-item>
    <el-form-item label="约定验收时间" prop="checkdate">
      <el-input v-model="dataForm.checkdate" placeholder="约定验收时间"></el-input>
    </el-form-item>
    <el-form-item label="是否有硬件-是/否" prop="hardware">
      <el-input v-model="dataForm.hardware" placeholder="是否有硬件-是/否"></el-input>
    </el-form-item>
    <el-form-item label="质保期-单位-月" prop="warranty">
      <el-input v-model="dataForm.warranty" placeholder="质保期-单位-月"></el-input>
    </el-form-item>
    <el-form-item label="回款条件一" prop="paymentCondition1">
      <el-input v-model="dataForm.paymentCondition1" placeholder="回款条件一"></el-input>
    </el-form-item>
    <el-form-item label="回款时间一" prop="paymentDate1">
      <el-input v-model="dataForm.paymentDate1" placeholder="回款时间一"></el-input>
    </el-form-item>
    <el-form-item label="回款条件三" prop="paymentCondition2">
      <el-input v-model="dataForm.paymentCondition2" placeholder="回款条件三"></el-input>
    </el-form-item>
    <el-form-item label="回款时间三" prop="paymentDate2">
      <el-input v-model="dataForm.paymentDate2" placeholder="回款时间三"></el-input>
    </el-form-item>
    <el-form-item label="${column.comments}" prop="paymentCondition3">
      <el-input v-model="dataForm.paymentCondition3" placeholder="${column.comments}"></el-input>
    </el-form-item>
    <el-form-item label="${column.comments}" prop="paymentDate3">
      <el-input v-model="dataForm.paymentDate3" placeholder="${column.comments}"></el-input>
    </el-form-item>
    <el-form-item label="是否续签维护合同-新的项目编号" prop="mainConid">
      <el-input v-model="dataForm.mainConid" placeholder="是否续签维护合同-新的项目编号"></el-input>
    </el-form-item>
    <el-form-item label="${column.comments}" prop="approver">
      <el-input v-model="dataForm.approver" placeholder="${column.comments}"></el-input>
    </el-form-item>
    <el-form-item label="录入人" prop="joinname">
      <el-input v-model="dataForm.joinname" placeholder="录入人"></el-input>
    </el-form-item>
    <el-form-item label="录入时间" prop="jointime">
      <el-input v-model="dataForm.jointime" placeholder="录入时间"></el-input>
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
        conName: '',
        proId: '',
        area: '',
        proFirstParty: '',
        lastUser: '',
        productionDep: '',
        mainFunction: '',
        signdate: '',
        checkdate: '',
        hardware: '',
        warranty: '',
        paymentCondition1: '',
        paymentDate1: '',
        paymentCondition2: '',
        paymentDate2: '',
        paymentCondition3: '',
        paymentDate3: '',
        mainConid: '',
        approver: '',
        joinname: '',
        jointime: ''
      },
      dataRule: {
        conName: [
          { required: true, message: '合同名称不能为空', trigger: 'blur' }
        ],
        proId: [
          { required: true, message: '项目编号不能为空', trigger: 'blur' }
        ],
        area: [
          { required: true, message: '所属区域不能为空', trigger: 'blur' }
        ],
        proFirstParty: [
          { required: true, message: '项目甲方不能为空', trigger: 'blur' }
        ],
        lastUser: [
          { required: true, message: '最终用户不能为空', trigger: 'blur' }
        ],
        productionDep: [
          { required: true, message: '所属产品部不能为空', trigger: 'blur' }
        ],
        mainFunction: [
          { required: true, message: '主要功能点不能为空', trigger: 'blur' }
        ],
        signdate: [
          { required: true, message: '合同签订时间不能为空', trigger: 'blur' }
        ],
        checkdate: [
          { required: true, message: '约定验收时间不能为空', trigger: 'blur' }
        ],
        hardware: [
          { required: true, message: '是否有硬件-是/否不能为空', trigger: 'blur' }
        ],
        warranty: [
          { required: true, message: '质保期-单位-月不能为空', trigger: 'blur' }
        ],
        paymentCondition1: [
          { required: true, message: '回款条件一不能为空', trigger: 'blur' }
        ],
        paymentDate1: [
          { required: true, message: '回款时间一不能为空', trigger: 'blur' }
        ],
        paymentCondition2: [
          { required: true, message: '回款条件三不能为空', trigger: 'blur' }
        ],
        paymentDate2: [
          { required: true, message: '回款时间三不能为空', trigger: 'blur' }
        ],
        paymentCondition3: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        paymentDate3: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        mainConid: [
          { required: true, message: '是否续签维护合同-新的项目编号不能为空', trigger: 'blur' }
        ],
        approver: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        joinname: [
          { required: true, message: '录入人不能为空', trigger: 'blur' }
        ],
        jointime: [
          { required: true, message: '录入时间不能为空', trigger: 'blur' }
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
            url: this.$http.adornUrl(`/user/ctcontractinfo/info/${this.dataForm.id}`),
            method: 'get',
            params: this.$http.adornParams()
          }).then(({data}) => {
            if (data && data.code === 0) {
              this.dataForm.conName = data.ctContractInfo.conName
              this.dataForm.proId = data.ctContractInfo.proId
              this.dataForm.area = data.ctContractInfo.area
              this.dataForm.proFirstParty = data.ctContractInfo.proFirstParty
              this.dataForm.lastUser = data.ctContractInfo.lastUser
              this.dataForm.productionDep = data.ctContractInfo.productionDep
              this.dataForm.mainFunction = data.ctContractInfo.mainFunction
              this.dataForm.signdate = data.ctContractInfo.signdate
              this.dataForm.checkdate = data.ctContractInfo.checkdate
              this.dataForm.hardware = data.ctContractInfo.hardware
              this.dataForm.warranty = data.ctContractInfo.warranty
              this.dataForm.paymentCondition1 = data.ctContractInfo.paymentCondition1
              this.dataForm.paymentDate1 = data.ctContractInfo.paymentDate1
              this.dataForm.paymentCondition2 = data.ctContractInfo.paymentCondition2
              this.dataForm.paymentDate2 = data.ctContractInfo.paymentDate2
              this.dataForm.paymentCondition3 = data.ctContractInfo.paymentCondition3
              this.dataForm.paymentDate3 = data.ctContractInfo.paymentDate3
              this.dataForm.mainConid = data.ctContractInfo.mainConid
              this.dataForm.approver = data.ctContractInfo.approver
              this.dataForm.joinname = data.ctContractInfo.joinname
              this.dataForm.jointime = data.ctContractInfo.jointime
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
            url: this.$http.adornUrl(`/user/ctcontractinfo/${!this.dataForm.id ? 'save' : 'update'}`),
            method: 'post',
            data: this.$http.adornData({
              'id': this.dataForm.id || undefined,
              'conName': this.dataForm.conName,
              'proId': this.dataForm.proId,
              'area': this.dataForm.area,
              'proFirstParty': this.dataForm.proFirstParty,
              'lastUser': this.dataForm.lastUser,
              'productionDep': this.dataForm.productionDep,
              'mainFunction': this.dataForm.mainFunction,
              'signdate': this.dataForm.signdate,
              'checkdate': this.dataForm.checkdate,
              'hardware': this.dataForm.hardware,
              'warranty': this.dataForm.warranty,
              'paymentCondition1': this.dataForm.paymentCondition1,
              'paymentDate1': this.dataForm.paymentDate1,
              'paymentCondition2': this.dataForm.paymentCondition2,
              'paymentDate2': this.dataForm.paymentDate2,
              'paymentCondition3': this.dataForm.paymentCondition3,
              'paymentDate3': this.dataForm.paymentDate3,
              'mainConid': this.dataForm.mainConid,
              'approver': this.dataForm.approver,
              'joinname': this.dataForm.joinname,
              'jointime': this.dataForm.jointime
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
