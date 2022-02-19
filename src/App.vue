<template>
  <div id="app" class="d-flex justify-content-center align-items-center">
    <div>
      <GenForm @TableData="parseData" class="mb-3" />
      <Table :tableData="this.parseTableData" :tableLimit="this.tableLimit" />
    </div>
    <div class="d-flex flex-column justify-content-center align-items-center">
      <Diagramm
        :tableData="this.parseTableData"
        :rands="this.rands"
        class="mb-3"
      />
      <download-csv
        :data="this.parseTableData"
        v-if="parseTableData.length > 0"
        class="btn"
      >
        Download Data
        <img src="../src/assets/csv-file.svg" width="20px" />
      </download-csv>
    </div>
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
      parseTableData: [],
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
