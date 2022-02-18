<template>
  <div id="app" class="d-flex justify-content-center align-items-center">
    <div>
      <GenForm @TableData="parseData" class="mb-3" />
      <Table :tableData="this.parseTableData" :tableLimit="this.tableLimit" />
    </div>
    <Diagramm :tableData="this.parseTableData" :rands="this.rands" />
  </div>
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
  margin-top: 50px;
}
</style>
