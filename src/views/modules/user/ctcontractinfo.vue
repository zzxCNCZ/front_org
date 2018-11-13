<template>
  <div class="mod-config">
    <el-form :inline="true" :model="dataForm" @keyup.enter.native="getDataList()">
      <el-form-item>
        <el-input v-model="dataForm.key" placeholder="参数名" clearable></el-input>
      </el-form-item>
      <el-form-item>
        <el-button @click="getDataList()">查询</el-button>
        <el-button v-if="isAuth('user:ctcontractinfo:save')" type="primary" @click="addOrUpdateHandle()">新增</el-button>
        <el-button v-if="isAuth('user:ctcontractinfo:delete')" type="danger" @click="deleteHandle()" :disabled="dataListSelections.length <= 0">批量删除</el-button>
      </el-form-item>
    </el-form>
    <el-table
      :data="dataList"
      border
      v-loading="dataListLoading"
      @selection-change="selectionChangeHandle"
      style="width: 100%;">
      <el-table-column
        type="selection"
        header-align="center"
        align="center"
        width="50">
      </el-table-column>
      <el-table-column
        prop="id"
        header-align="center"
        align="center"
        label="合同编号">
      </el-table-column>
      <el-table-column
        prop="conName"
        header-align="center"
        align="center"
        label="合同名称">
      </el-table-column>
      <el-table-column
        prop="proId"
        header-align="center"
        align="center"
        label="项目编号">
      </el-table-column>
      <el-table-column
        prop="area"
        header-align="center"
        align="center"
        label="所属区域">
      </el-table-column>
      <el-table-column
        prop="proFirstParty"
        header-align="center"
        align="center"
        label="项目甲方">
      </el-table-column>
      <el-table-column
        prop="lastUser"
        header-align="center"
        align="center"
        label="最终用户">
      </el-table-column>
      <el-table-column
        prop="productionDep"
        header-align="center"
        align="center"
        label="所属产品部">
      </el-table-column>
      <el-table-column
        prop="mainFunction"
        header-align="center"
        align="center"
        label="主要功能点">
      </el-table-column>
      <el-table-column
        prop="signdate"
        header-align="center"
        align="center"
        label="合同签订时间">
      </el-table-column>
      <el-table-column
        prop="checkdate"
        header-align="center"
        align="center"
        label="约定验收时间">
      </el-table-column>
      <el-table-column
        prop="hardware"
        header-align="center"
        align="center"
        label="是否有硬件-是/否">
      </el-table-column>
      <el-table-column
        prop="warranty"
        header-align="center"
        align="center"
        label="质保期-单位-月">
      </el-table-column>
      <el-table-column
        prop="paymentCondition1"
        header-align="center"
        align="center"
        label="回款条件一">
      </el-table-column>
      <el-table-column
        prop="paymentDate1"
        header-align="center"
        align="center"
        label="回款时间一">
      </el-table-column>
      <el-table-column
        prop="paymentCondition2"
        header-align="center"
        align="center"
        label="回款条件三">
      </el-table-column>
      <el-table-column
        prop="paymentDate2"
        header-align="center"
        align="center"
        label="回款时间三">
      </el-table-column>
      <el-table-column
        prop="paymentCondition3"
        header-align="center"
        align="center"
        label="${column.comments}">
      </el-table-column>
      <el-table-column
        prop="paymentDate3"
        header-align="center"
        align="center"
        label="${column.comments}">
      </el-table-column>
      <el-table-column
        prop="mainConid"
        header-align="center"
        align="center"
        label="是否续签维护合同-新的项目编号">
      </el-table-column>
      <el-table-column
        prop="approver"
        header-align="center"
        align="center"
        label="${column.comments}">
      </el-table-column>
      <el-table-column
        prop="joinname"
        header-align="center"
        align="center"
        label="录入人">
      </el-table-column>
      <el-table-column
        prop="jointime"
        header-align="center"
        align="center"
        label="录入时间">
      </el-table-column>
      <el-table-column
        fixed="right"
        header-align="center"
        align="center"
        width="150"
        label="操作">
        <template slot-scope="scope">
          <el-button type="text" size="small" @click="addOrUpdateHandle(scope.row.id)">修改</el-button>
          <el-button type="text" size="small" @click="deleteHandle(scope.row.id)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
    <el-pagination
      @size-change="sizeChangeHandle"
      @current-change="currentChangeHandle"
      :current-page="pageIndex"
      :page-sizes="[10, 20, 50, 100]"
      :page-size="pageSize"
      :total="totalPage"
      layout="total, sizes, prev, pager, next, jumper">
    </el-pagination>
    <!-- 弹窗, 新增 / 修改 -->
    <add-or-update v-if="addOrUpdateVisible" ref="addOrUpdate" @refreshDataList="getDataList"></add-or-update>
  </div>
</template>

<script>
import AddOrUpdate from './ctcontractinfo-add-or-update'
export default {
  data () {
    return {
      dataForm: {
        key: ''
      },
      dataList: [],
      pageIndex: 1,
      pageSize: 10,
      totalPage: 0,
      dataListLoading: false,
      dataListSelections: [],
      addOrUpdateVisible: false
    }
  },
  components: {
    AddOrUpdate
  },
  activated () {
    this.getDataList()
  },
  methods: {
    // 获取数据列表
    getDataList () {
      this.dataListLoading = true
      this.$http({
        url: this.$http.adornUrl('/user/ctcontractinfo/list'),
        method: 'get',
        params: this.$http.adornParams({
          'page': this.pageIndex,
          'limit': this.pageSize,
          'key': this.dataForm.key
        })
      }).then(({data}) => {
        if (data && data.code === 0) {
          this.dataList = data.page.list
          this.totalPage = data.page.totalCount
        } else {
          this.dataList = []
          this.totalPage = 0
        }
        this.dataListLoading = false
      })
    },
    // 每页数
    sizeChangeHandle (val) {
      this.pageSize = val
      this.pageIndex = 1
      this.getDataList()
    },
    // 当前页
    currentChangeHandle (val) {
      this.pageIndex = val
      this.getDataList()
    },
    // 多选
    selectionChangeHandle (val) {
      this.dataListSelections = val
    },
    // 新增 / 修改
    addOrUpdateHandle (id) {
      this.addOrUpdateVisible = true
      this.$nextTick(() => {
        this.$refs.addOrUpdate.init(id)
      })
    },
    // 删除
    deleteHandle (id) {
      var ids = id ? [id] : this.dataListSelections.map(item => {
        return item.id
      })
      this.$confirm(`确定对[id=${ids.join(',')}]进行[${id ? '删除' : '批量删除'}]操作?`, '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => {
        this.$http({
          url: this.$http.adornUrl('/user/ctcontractinfo/delete'),
          method: 'post',
          data: this.$http.adornData(ids, false)
        }).then(({data}) => {
          if (data && data.code === 0) {
            this.$message({
              message: '操作成功',
              type: 'success',
              duration: 1500,
              onClose: () => {
                this.getDataList()
              }
            })
          } else {
            this.$message.error(data.msg)
          }
        })
      })
    }
  }
}
</script>
