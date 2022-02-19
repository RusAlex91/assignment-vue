<template>
  <div id="app" class="d-flex justify-content-center align-items-center">
    <div>
      <GenForm @TableData="parseData" class="mb-3" />
      <Table :tableData="this.parseTableData" :tableLimit="this.tableLimit" />
    </div>
    <div class="d-flex flex-column justify-content-center align-items-center">
      <select v-model="type">
        <option value="pie-chart">Pie</option>
        <option value="bar-chart">Bar</option>
      </select>
      <component
        :tableData="this.parseTableData"
        :rands="this.rands"
        class="mb-3"
        :is="type"
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
import PieChart from './components/PieChart.vue'
import BarChart from './components/BarChart.vue'

export default {
  name: 'App',
  components: {
    GenForm,
    Table,
    PieChart,
    BarChart
  },
  data () {
    return {
      parseTableData: [],
      tableLimit: null,
      rands: null,
      type: 'pie-chart'
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
