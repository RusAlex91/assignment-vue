<template>
  <GenForm @TableData="parseData" />
  <Table :tableData="this.parseTableData" :tableLimit="this.tableLimit" />
  <Diagramm :tableData="this.parseTableData" :rands="this.rands" />
</template>

<script>
import GenForm from './components/GenForm.vue'
import Table from './components/Table.vue'
import Diagramm from './components/Diagramm.vue'

export default {
  name: 'App',
  components: {
    GenForm,
    Table,
    Diagramm
  },
  data () {
    return {
      parseTableData: null,
      tableLimit: null,
      rands: null
    }
  },
  methods: {
    parseData ({ JSONData, tableLimit, rands }) {
      this.parseTableData = JSON.parse(JSONData)
      this.tableLimit = tableLimit
      this.rands = rands
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
