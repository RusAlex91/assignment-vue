<template>
  <div class="table-wrapper">
    <div class="table">
      <table>
        <tr>
          <th>id</th>
          <th>name</th>
          <th>rand</th>
        </tr>
        <tr v-for="entry in updatedTableData" :key="entry.id">
          <td>{{ entry.id }}</td>
          <td>{{ entry.title }}</td>
          <td>{{ entry.rand }}</td>
        </tr>
      </table>
    </div>
    <div class="table-controls">
      <button @click="prevTablePage" class="pag-button">-5</button>
      <button @click="nextTablePage" class="pag-button">+5</button>
      <div class="pagination" v-for="page in pageCount" :key="page">
        <button @click="toPage(page)">{{ page }}</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    tableData: {
      type: Array,
      default: () => []
    },
    tableLimit: {
      type: Number,
      default: 0
    }
  },
  data () {
    return {
      dataTable: null,
      limit: 0,
      updatedTableData: null,
      updatedLimit: null,
      pageCount: null
    }
  },
  watch: {
    tableData (newValue, oldValue) {
      this.dataTable = this.tableData
      this.pageCount = this.tableData.length / this.tableLimit
    },
    tableLimit () {
      this.limit = this.tableLimit
      this.updatedLimit = this.tableLimit
      this.limitedData()
    }
  },
  methods: {
    prevTablePage () {
      const newLimit = this.updatedLimit - this.limit
      const prevLimit = this.updatedLimit - this.limit - this.limit
      // if (newLimit === 0) {
      //   newLimit = this.limit
      // }
      this.updateLimit(newLimit, prevLimit)
      this.updatedLimit = newLimit
    },
    nextTablePage () {
      const newLimit = this.updatedLimit + this.limit
      const prevLimit = this.updatedLimit
      this.updateLimit(newLimit, prevLimit)
      this.updatedLimit = newLimit
    },
    updateLimit (newLimit, prevLimit) {
      const dataTable = this.dataTable
      this.updatedTableData = dataTable.slice(prevLimit, newLimit)
    },
    limitedData () {
      const dataTable = this.dataTable
      this.updatedTableData = dataTable.slice(0, this.updatedLimit)
    },
    toPage (num) {
      debugger
      const dataTable = this.dataTable
      const prevLimit = (num - 1) * this.limit
      const newLimit = prevLimit + this.limit
      this.updatedTableData = dataTable.slice(prevLimit, newLimit)
    }
  }
}
</script>

<style></style>
