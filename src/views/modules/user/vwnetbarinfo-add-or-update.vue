<template>
  <el-dialog
    :title="!dataForm.id ? '新增' : '修改'"
    :close-on-click-modal="false"
    :visible.sync="visible">
    <el-form :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmit()" label-width="80px">
    <el-form-item label="" prop="lat">
      <el-input v-model="dataForm.lat" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="lon">
      <el-input v-model="dataForm.lon" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="tbXlbh">
      <el-input v-model="dataForm.tbXlbh" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="rksj">
      <el-input v-model="dataForm.rksj" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="toIp">
      <el-input v-model="dataForm.toIp" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="fromIp">
      <el-input v-model="dataForm.fromIp" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="orgCode">
      <el-input v-model="dataForm.orgCode" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="regionalism">
      <el-input v-model="dataForm.regionalism" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="remark">
      <el-input v-model="dataForm.remark" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="netMonitorManTel">
      <el-input v-model="dataForm.netMonitorManTel" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="netMonitorMan">
      <el-input v-model="dataForm.netMonitorMan" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="netMonitorDepartment">
      <el-input v-model="dataForm.netMonitorDepartment" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="practitionerNumber">
      <el-input v-model="dataForm.practitionerNumber" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="netType">
      <el-input v-model="dataForm.netType" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="ip">
      <el-input v-model="dataForm.ip" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="serverNumber">
      <el-input v-model="dataForm.serverNumber" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="endingNumber">
      <el-input v-model="dataForm.endingNumber" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="status">
      <el-input v-model="dataForm.status" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="producerCode">
      <el-input v-model="dataForm.producerCode" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="inforManEmail">
      <el-input v-model="dataForm.inforManEmail" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="inforManTel">
      <el-input v-model="dataForm.inforManTel" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="inforMan">
      <el-input v-model="dataForm.inforMan" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="principalTel">
      <el-input v-model="dataForm.principalTel" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="principal">
      <el-input v-model="dataForm.principal" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="zip">
      <el-input v-model="dataForm.zip" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="address">
      <el-input v-model="dataForm.address" placeholder=""></el-input>
    </el-form-item>
    <el-form-item label="" prop="serviceName">
      <el-input v-model="dataForm.serviceName" placeholder=""></el-input>
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
        lat: '',
        lon: '',
        tbXlbh: '',
        rksj: '',
        toIp: '',
        fromIp: '',
        orgCode: '',
        regionalism: '',
        remark: '',
        netMonitorManTel: '',
        netMonitorMan: '',
        netMonitorDepartment: '',
        practitionerNumber: '',
        netType: '',
        ip: '',
        serverNumber: '',
        endingNumber: '',
        status: '',
        producerCode: '',
        inforManEmail: '',
        inforManTel: '',
        inforMan: '',
        principalTel: '',
        principal: '',
        zip: '',
        address: '',
        serviceName: '',
        serviceCode: 0
      },
      dataRule: {
        lat: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        lon: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        tbXlbh: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        rksj: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        toIp: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        fromIp: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        orgCode: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        regionalism: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        remark: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        netMonitorManTel: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        netMonitorMan: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        netMonitorDepartment: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        practitionerNumber: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        netType: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        ip: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        serverNumber: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        endingNumber: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        status: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        producerCode: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        inforManEmail: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        inforManTel: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        inforMan: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        principalTel: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        principal: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        zip: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        address: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ],
        serviceName: [
          { required: true, message: '不能为空', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    init (id) {
      this.dataForm.serviceCode = id || 0
      this.visible = true
      this.$nextTick(() => {
        this.$refs['dataForm'].resetFields()
        if (this.dataForm.serviceCode) {
          this.$http({
            url: this.$http.adornUrl(`/user/vwnetbarinfo/info/${this.dataForm.serviceCode}`),
            method: 'get',
            params: this.$http.adornParams()
          }).then(({data}) => {
            if (data && data.code === 0) {
              this.dataForm.lat = data.vwNetbarInfo.lat
              this.dataForm.lon = data.vwNetbarInfo.lon
              this.dataForm.tbXlbh = data.vwNetbarInfo.tbXlbh
              this.dataForm.rksj = data.vwNetbarInfo.rksj
              this.dataForm.toIp = data.vwNetbarInfo.toIp
              this.dataForm.fromIp = data.vwNetbarInfo.fromIp
              this.dataForm.orgCode = data.vwNetbarInfo.orgCode
              this.dataForm.regionalism = data.vwNetbarInfo.regionalism
              this.dataForm.remark = data.vwNetbarInfo.remark
              this.dataForm.netMonitorManTel = data.vwNetbarInfo.netMonitorManTel
              this.dataForm.netMonitorMan = data.vwNetbarInfo.netMonitorMan
              this.dataForm.netMonitorDepartment = data.vwNetbarInfo.netMonitorDepartment
              this.dataForm.practitionerNumber = data.vwNetbarInfo.practitionerNumber
              this.dataForm.netType = data.vwNetbarInfo.netType
              this.dataForm.ip = data.vwNetbarInfo.ip
              this.dataForm.serverNumber = data.vwNetbarInfo.serverNumber
              this.dataForm.endingNumber = data.vwNetbarInfo.endingNumber
              this.dataForm.status = data.vwNetbarInfo.status
              this.dataForm.producerCode = data.vwNetbarInfo.producerCode
              this.dataForm.inforManEmail = data.vwNetbarInfo.inforManEmail
              this.dataForm.inforManTel = data.vwNetbarInfo.inforManTel
              this.dataForm.inforMan = data.vwNetbarInfo.inforMan
              this.dataForm.principalTel = data.vwNetbarInfo.principalTel
              this.dataForm.principal = data.vwNetbarInfo.principal
              this.dataForm.zip = data.vwNetbarInfo.zip
              this.dataForm.address = data.vwNetbarInfo.address
              this.dataForm.serviceName = data.vwNetbarInfo.serviceName
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
            url: this.$http.adornUrl(`/user/vwnetbarinfo/${!this.dataForm.serviceCode ? 'save' : 'update'}`),
            method: 'post',
            data: this.$http.adornData({
              'lat': this.dataForm.lat,
              'lon': this.dataForm.lon,
              'tbXlbh': this.dataForm.tbXlbh,
              'rksj': this.dataForm.rksj,
              'toIp': this.dataForm.toIp,
              'fromIp': this.dataForm.fromIp,
              'orgCode': this.dataForm.orgCode,
              'regionalism': this.dataForm.regionalism,
              'remark': this.dataForm.remark,
              'netMonitorManTel': this.dataForm.netMonitorManTel,
              'netMonitorMan': this.dataForm.netMonitorMan,
              'netMonitorDepartment': this.dataForm.netMonitorDepartment,
              'practitionerNumber': this.dataForm.practitionerNumber,
              'netType': this.dataForm.netType,
              'ip': this.dataForm.ip,
              'serverNumber': this.dataForm.serverNumber,
              'endingNumber': this.dataForm.endingNumber,
              'status': this.dataForm.status,
              'producerCode': this.dataForm.producerCode,
              'inforManEmail': this.dataForm.inforManEmail,
              'inforManTel': this.dataForm.inforManTel,
              'inforMan': this.dataForm.inforMan,
              'principalTel': this.dataForm.principalTel,
              'principal': this.dataForm.principal,
              'zip': this.dataForm.zip,
              'address': this.dataForm.address,
              'serviceName': this.dataForm.serviceName,
              'serviceCode': this.dataForm.serviceCode || undefined
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
