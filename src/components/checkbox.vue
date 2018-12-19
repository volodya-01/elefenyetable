<template>
 <div>
    <div>
     <el-table ref="multipleTable" :data="appList" border tooltip-effect="dark" style="width: 100%;height: 380px;overflow:auto"
     @selection-change="changeFun">
     <el-table-column type="selection" width="55" class="selection" prop='uuid' :selectable='checkboxInit' @selection-change="changeFun">
       </el-table-column>
       <el-table-column label="">
         <template slot-scope="scope"></template>
         </el-table-column>
         <el-table-column prop="username" label="username"></el-table-column>
         <el-table-column prop="createTime" label="创建时间"></el-table-column>
         </el-table>

  </div>


  
 </div>
</template>
<script>
export default {
  name:"Checkbox",
  data(){
    return{
multipleSelection:[]
    }
  },
  methods:{
    //复选框状态改变
    changeFun(val) {
      this.multipleSelection = val;
      console.log(this.multipleSelection)
    },
  }
}
</script>


