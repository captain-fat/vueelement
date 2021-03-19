<template>
  <div>
    <el-table
        :data="tableData"
        border
        style="width: 100%">
      <el-table-column
          fixed
          prop="id"
          label="股票id"
          width="150">
      </el-table-column>
      <el-table-column
          prop="name"
          label="股票名"
          width="120">
      </el-table-column>
      <el-table-column
          prop="price"
          label="股票价格"
          width="120">
      </el-table-column>
      <el-table-column
          prop="rate"
          label="股票涨跌"
          width="120">
      </el-table-column>
      <el-table-column

          label="操作"
          width="100">
        <template slot-scope="scope">
          <el-button @click="handleClick(scope.row)" type="text" size="small">查看</el-button>
          <el-button type="text" size="small">编辑</el-button>
        </template>
      </el-table-column>
    </el-table>
    <el-pagination
        background
        layout="prev, pager, next"
        :page-size="3"
        :total="30"
        @current-change="page">
    </el-pagination>
  </div>
</template>

<script>
export default {
  methods: {
    handleClick(row) {
      console.log(row);
    },
    page(currentPage){
      const _this = this;
      axios.get('http://localhost:8081/stock/findAll/'+(currentPage-1)+
      _this.tableData=resp.data.content;
      )
    }
  },

  data() {
    return {
      tableData: [{
        id: 1,
        name: '科技股',
        price: 45.43,
        rate: +1.57,
      }, {
        id: 2,
        name: '教育股',
        price: 35.22,
        rate: +0.19,
      }, {
        id: 3,
        name: '石油股',
        price: 45.43,
        rate: -4.61,
      }, {
        id: 4,
        name: '餐饮股',
        price: 55.43,
        rate: -9.77,
      }]
    }
  },
  created() {
    const _this = this;
    axios.get("http://localhost:8081/stock/findAll/0/3").then(function (resp){
      _this.tableData=resp.data.content;
    })
  }

}


</script>