<template>
<div>
    <div>
    <el-checkbox v-model="checked3" label="备选项1" border @change="selecteChange(checked3)"></el-checkbox>
    <el-checkbox v-model="checked4" label="备选项2" border></el-checkbox>
  </div>
  <div style="margin-top: 20px">
    <el-checkbox v-model="checked5" label="备选项1" border size="medium"></el-checkbox>
    <el-checkbox v-model="checked6" label="备选项2" border size="medium"></el-checkbox>
  </div>
  <div style="margin-top: 20px">
    <el-checkbox-group v-model="checkboxGroup5" size="small">
      <el-checkbox label="备选项1" border></el-checkbox>
      <el-checkbox label="备选项2" border disabled></el-checkbox>
    </el-checkbox-group>
  </div>
  <div style="margin-top: 20px">
    <el-checkbox-group v-model="checkboxGroup6" size="mini" disabled>
      <el-checkbox label="备选项1" border></el-checkbox>
      <el-checkbox label="备选项2" border></el-checkbox>
    </el-checkbox-group>
  </div>
</div>
</template>

<script>
  export default {
    name:"Checkbox3",
    data () {
      return {
        checked3: true,
        checked4: false,
        checked5: false,
        checked6: true,
        checkboxGroup5: [],
        checkboxGroup6: []
      };
    },
    methods:{
     selecteChange(){
        console.log(checked3)
      }
    }
  }
</script>

