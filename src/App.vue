<template>
  <GenForm @TableData="parseData" />
  <Table :tableData="this.parseTableData" :tableLimit="this.tableLimit" />
</template>

<script>
import GenForm from './components/GenForm.vue'
import Table from './components/Table.vue'

export default {
  name: 'App',
  components: {
    GenForm,
    Table
  },
  data () {
    return {
      parseTableData: null,
      tableLimit: null
    }
  },
  methods: {
    parseData ({ JSONData, tableLimit }) {
      this.parseTableData = JSON.parse(JSONData)
      this.tableLimit = tableLimit
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
