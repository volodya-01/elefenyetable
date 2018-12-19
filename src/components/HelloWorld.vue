<template>
  <div class="hello">
    <!-- <Table/> -->
        <!-- <Table2/> -->
          <Table3/>
          <Checkbox/>
          <Checkbox2/>
          <Checkbox3/>
  </div>
</template>

<script>
/* import Table from '@/components/table' */
/* import Table2 from '@/components/table2' */
import Table3 from '@/components/table3'
import Checkbox from '@/components/checkbox'
import Checkbox2 from '@/components/checkbox2'
import Checkbox3 from '@/components/checkbox3'
export default {
  name: 'HelloWorld',
  components:{
   /*  Table, */
    /* Table2, */
     Table3,
     Checkbox,
         Checkbox2,
         Checkbox3
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
