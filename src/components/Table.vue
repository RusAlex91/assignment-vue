<template>
  <div class="table-wrapper">
    <b-table
      id="main-table"
      striped
      hover
      :per-page="this.limit"
      :items="dataTable"
      :fields="fields"
      :current-page="currentPage"
    ></b-table>
    <b-pagination
      v-model="currentPage"
      :total-rows="this.tableLength"
      :per-page="this.limit"
      aria-controls="main-table"
    ></b-pagination>
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
      fields: [
        { key: 'id', sortable: true },
        { key: 'title', sortable: true },
        { key: 'rand', sortable: true }
      ],
      currentPage: 1,
      pagPerPage: 1,
      tableLength: null
    }
  },
  watch: {
    tableData () {
      this.dataTable = this.tableData
    },
    tableLimit () {
      this.limit = this.tableLimit
      this.tableLength = this.dataTable.length
    }
  }
}
</script>

<style></style>
