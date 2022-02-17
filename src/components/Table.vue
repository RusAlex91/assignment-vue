<template>
  <div class="table-wrapper">
    <div class="table">
      <table>
        <tr>
          <th>id</th>
          <th>name</th>
          <th>rand</th>
        </tr>
        <tr v-for="entry in computedObj" :key="entry.id">
          <td>{{ entry.id }}</td>
          <td>{{ entry.title }}</td>
          <td>{{ entry.rand }}</td>
        </tr>
      </table>
    </div>
    <div class="table-controls">
      <button class="pag-button">&rarr</button>
      <button class="pag-button">&larr</button>
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
      limit: null
    }
  },
  watch: {
    tableData (newValue, oldValue) {
      this.dataTable = this.tableData
    },
    tableLimit () {
      this.limit = this.tableLimit
    }
  },
  computed: {
    computedObj () {
      return this.limit ? this.dataTable.slice(0, this.limit) : this.dataTable
    }
  }
}
</script>

<style></style>
