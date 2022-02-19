<script>
import { Bar } from 'vue-chartjs'

export default {
  extends: Bar,
  props: {
    tableData: {
      type: Array,
      default: null
    },
    rands: {
      type: String,
      default: null
    }
  },
  watch: {
    rands () {
      this.createDiagramm()
    }
  },
  methods: {
    createDiagramm () {
      // eslint-disable-next-line no-debugger

      const data = this.tableData

      const uniqRand = this.rands.split(',')
      const datasets = []
      uniqRand.forEach((element, index) => {
        const filteredArray = data.filter(
          uniq => uniq.rand === `${uniqRand[index]}`
        )
        const filteredLength = filteredArray.length

        const set = {
          label: uniqRand[index],
          backgroundColor:
            '#' + Math.floor(Math.random() * 16777215).toString(16),
          data: [filteredLength]
        }
        datasets.push(set)
      })

      this.renderChart({ datasets })
    }
  },
  mounted () {
    if (this.rands !== null) {
      this.createDiagramm()
    }
  }
}
</script>

<style>
canvas {
  width: 100%;
  height: 100%;
}
.canvas-wrapper {
  width: 300px;
  height: 300px;
}
</style>
