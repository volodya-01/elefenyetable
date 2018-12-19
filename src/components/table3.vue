<template>
  <div class="outbox">
     <div class="tablebox">
          <el-table
            :cell-class-name="rowClass"
            :data="info"
            v-if="!isHidden"
            border-top
            empty-text
            style="width: 100%" stripe :header-cell-style="headerStyle" :row-style="rowStyle" height="100%"
            v-loading="loading" element-loading-text="拼命加载中"
          element-loading-spinner="el-icon-loading" element-loading-background="rgba(143, 188, 143, 0.8)"
             >
                <el-table-column class="red"
                prop="bh"
                label="编号"
               min-width="100">
                </el-table-column>
                <el-table-column
                prop="name"
                label="压力点名称"
               min-width="100">
               <template slot-scope="scope">
		<span v-if="scope.row.name=='0'">特级</span>
		<span v-if="scope.row.name=='1'">一级</span>
		<span v-if="scope.row.name=='2'">二级</span>
		<span v-else>{{scope.row.name}}</span>
	</template>
                </el-table-column>
                <el-table-column
                prop="mb"
                label="目标压力（MPa）"
                min-width="100">
                </el-table-column>
                <el-table-column
                prop="sj"
                label="实际压力"
                min-width="100">
                </el-table-column>
     </el-table>
</div>

    <div class="block">
        <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page.sync="currentPage1"
        :page-size="5"
        layout="prev, pager, next"
        :total="24">
        </el-pagination>
    </div>

    <div>
      
    </div>
  </div>

</template>

<script>
export default {
  name: "Table3",
  data() {
    return {
      info: [],
      headerStyle() {
        return {
          "background-color": "#f0f0f1",
          color: "#6e7b8b",
          "font-size": "12px",
          "font-family": "微软雅黑"
        };
      },
      rowStyle() {
        return {
          height: "40px",
          "line-height": "40px",
          color: "#6e7b8b"
        };
      },

      tableData: [
        {
          bh: "SZKKLLKK00012",
          name: "1",
          mb: "0.64",
          sj: "0.54"
        },
        {
          bh: "SZKKLLKK00012",
          name: "2",
          mb: "0.64",
          sj: "0.54"
        },
        {
          bh: "SZKKLLKK00012",
          name: "3",
          mb: "0.64",
          sj: "0.54"
        },
        {
          bh: "SZKKLLKK00012",
          name: "4",
          mb: "0.64",
          sj: "0.54"
        },
        {
          bh: "SZKKLLKK00012",
          name: "5",
          mb: "0.64",
          sj: "0.54"
        },
        {
          bh: "SZKKLLKK00012",
          name: "6",
          mb: "0.64",
          sj: "0.54"
        },
        {
          bh: "SZKKLLKK00012",
          name: "7",
          mb: "0.64",
          sj: "0.54"
        },
        {
          bh: "SZKKLLKK00012",
          name: "8",
          mb: "0.64",
          sj: "0.54"
        },
        {
          bh: "SZKKLLKK00012",
          name: "9",
          mb: "0.64",
          sj: "0.54"
        },
        {
          bh: "SZKKLLKK00012",
          name: "10",
          mb: "0.64",
          sj: "0.54"
        },
        {
          bh: "SZKKLLKK00012",
          name: "11",
          mb: "0.64",
          sj: "0.54"
        },
        {
          bh: "SZKKLLKK00012",
          name: "12",
          mb: "0.64",
          sj: "0.54"
        },
               {
          bh: "SZKKLLKK00012",
          name: "13",
          mb: "0.64",
          sj: "0.54"
        },
        {
          bh: "SZKKLLKK00012",
          name: "14",
          mb: "0.64",
          sj: "0.54"
        },
        {
          bh: "SZKKLLKK00012",
          name: "15",
          mb: "0.64",
          sj: "0.54"
        },
        {
          bh: "SZKKLLKK00012",
          name: "16",
          mb: "0.64",
          sj: "0.54"
        },
        {
          bh: "SZKKLLKK00012",
          name: "17",
          mb: "0.64",
          sj: "0.54"
        },
        {
          bh: "SZKKLLKK00012",
          name: "18",
          mb: "0.64",
          sj: "0.54"
        },
        {
          bh: "SZKKLLKK00012",
          name: "19",
          mb: "0.64",
          sj: "0.54"
        },
        {
          bh: "SZKKLLKK00012",
          name: "20",
          mb: "0.64",
          sj: "0.54"
        },
        {
          bh: "SZKKLLKK00012",
          name: "21",
          mb: "0.64",
          sj: "0.54"
        },
        {
          bh: "SZKKLLKK00012",
          name: "22",
          mb: "0.64",
          sj: "0.54"
        },
        {
          bh: "SZKKLLKK00012",
          name: "23",
          mb: "0.64",
          sj: "0.54"
        },
        {
          bh: "SZKKLLKK00012",
          name: "24",
          mb: "0.64",
          sj: "0.54"
        }
      ],

      currentPage: 1, //默认显示第一页
      pageSize: 10 //默认每页显示10条
    };
  },
  created() {
    this.info = this.tableData.slice(0, 5);
  },
  methods: {
    rowClass({ row, column, rowIndex, columnIndex }) {
      // if (rowIndex === 1 && columnIndex === 1) {
      //   return "red";
      // } else if (rowIndex === 6 && columnIndex === 4) {
      //   return "bacColorf4984e";
      // } else if (rowIndex === 6 && columnIndex === 5) {
      //   return "bacColor317eb0";
      // }
       if (row.name < 4 && columnIndex == 1) {
        return "red";
      }
    },
    /*    handleSizeChange(val) {
      console.log(`每页 ${val} 条`);
    }, */
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`);
      this.info = this.tableData.slice(5* val - 5, 5* val);
    },
    cell({ row, column, rowIndex, columnIndex }) {
      //第3列添加 red 类
      if (column == 2) {
        return "red";
      }
      //某一行其中的一个变量applies值如果大于0，并且在第六列，即确定一个具体的单元格需要确定行和列
      if (parseFloat(row.sj) > 0 && column == 2) {
        return "red";
      }
    }
  }
};
</script>
<style>
.tablebox {
  width: 70.66875vw;
  height: 45.077399vh;
}
.block {
  margin-top: 40px;
}
.red {
  color: #fff;
  background: red !important;
  width: 60px !important;
  height: 40px !important;
}
</style>

