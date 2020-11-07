<template>
  <el-table
    :data="tableData.filter(data => !search || data.deviceId.toLowerCase().includes(search.toLowerCase()))"
    border
    style="width: 100%">
    <el-table-column
      label="设备名"
      prop="deviceId">
    </el-table-column>
    <el-table-column
      label="设备类型"
      prop="type">
    </el-table-column>
    <el-table-column
      label="温度/℃"
      prop="temp">
    </el-table-column>
    <el-table-column
      align="right">
      <template slot="header" slot-scope="{}">
        <el-input
          v-model="search"
          size="mini"
          placeholder="输入设备名搜索"/>
      </template>
      <template slot-scope="scope">
        <el-button
          size="mini"
          type="primary"
          icon="el-icon-edit"
          @click="handleEdit(scope.$index, scope.row)">修改</el-button>
           <!-- scope.$index 获取当前行下标   scope.row 获取当前属性值 -->
        <el-button
          size="mini"
          icon="el-icon-share"
         @click="dialogTableVisible = true">查看</el-button>
         <el-dialog title="设备历史数据" :visible.sync="dialogTableVisible" align="left">
            <el-table :data="gridData">
                <el-table-column property="date" label="日期" width="290"></el-table-column>
                <el-table-column property="htemp" label="温度" width="300"></el-table-column>
            </el-table>
        </el-dialog>
        <el-button
          size="mini"
          type="danger"
          icon="el-icon-delete"
          @click="handleDelete(scope.$index, scope.row)">删除</el-button>
      </template>
    </el-table-column>
  </el-table>
</template>

<script>
  export default {
    data() {
      return {
        tableData: [{
          deviceId: '537852',
          type: 'air conditioner',
          temp: '26.7'
        }, {
          deviceId: '879864',
          type: 'air conditioner',
          temp: '27.8'
        }, {
          deviceId: '475348',
          type: 'air conditioner',
          temp: '25.5'
        }, {
          deviceId: '715287',
          type: 'air conditioner',
          temp: '23.9'
        }],

        gridData: [{
          date: '2016-05-02',
          htemp: '22.8',
        }, {
          date: '2016-05-04',
          htemp: '22.3',
        }, {
          date: '2016-05-01',
          htemp: '22.5',
        }, {
          date: '2016-05-03',
          htemp: '22.9',
        }],
        dialogTableVisible: false,
        dialogFormVisible: false,
        form: {
          name: '',
          region: '',
          date1: '',
          date2: '',
          delivery: false,
          type: [],
          resource: '',
          desc: ''
        },
        formLabelWidth: '120px',
        search: ''
      }
    },
    methods: {
      handleEdit(index, row) {
        console.log(index, row);
      },
      handleDelete(index, row) {
        console.log(index, row);
      }
    },
  }
</script>