<template>
  <div class="canvas-wrapper">
    <canvas ref="canvas"></canvas>
    <button @click="createDiagrammData()">Create</button>
  </div>
</template>

<script>
import { Pie } from 'vue-chartjs'

export default {
  extends: Pie,
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
  data () {},
  methods: {
    createDiagrammData () {
      const data = this.tableData
      const diagrammData = []
      // const key = 'rand'
      // const uniqeData = [
      //   ...new Map(data.map(item => [item[key], item])).values()
      // ]
      const uniqRand = this.rands.split(',')
      uniqRand.forEach((element, index) => {
        const filteredArray = data.filter(
          uniq => uniq.rand === `${uniqRand[index]}`
        )
        const filteredLength = filteredArray.length
        diagrammData.push(filteredLength)
      })

      // console.log(uniqeData)
      console.log(diagrammData)
      this.renderChart(
        {
          labels: uniqRand,
          datasets: [
            {
              label: '# of Rand',
              data: diagrammData,
              backgroundColor: [
                'rgba(255, 99, 132, 0.2)',
                'rgba(54, 162, 235, 0.2)',
                'rgba(255, 206, 86, 0.2)',
                'rgba(75, 192, 192, 0.2)',
                'rgba(153, 102, 255, 0.2)',
                'rgba(255, 159, 64, 0.2)'
              ],
              borderColor: [
                'rgba(255, 99, 132, 1)',
                'rgba(54, 162, 235, 1)',
                'rgba(255, 206, 86, 1)',
                'rgba(75, 192, 192, 1)',
                'rgba(153, 102, 255, 1)',
                'rgba(255, 159, 64, 1)'
              ],
              borderWidth: 1
            }
          ]
        },
        {
          responsive: true,
          maintainAspectRatio: false
        }
      )
    }
  },
  mounted () {}
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
