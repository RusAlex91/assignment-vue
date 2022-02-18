<template>
  <div class="">
    <form action="" v-on:submit.prevent>
      <input
        placeholder="0"
        v-model="recordsCount"
        type="number"
        class="records-number"
      />
      <input
        placeholder="0"
        v-model="onPageCount"
        type="number"
        class="onpage-number"
      />
      <input
        placeholder="apple, tomato"
        v-model="randWords"
        type="text"
        class="rand-words"
      />
      <button @click="applyData" class="apply">Подтвердить</button>
      <button @click="resetData" class="reset">Сбросить</button>
    </form>
  </div>
</template>

<script>
export default {
  data () {
    return {
      recordsCount: null,
      onPageCount: null,
      randWords: null,
      preJSONdata: null,
      JSONData: null
    }
  },
  methods: {
    applyData () {
      this.generateData()
      this.generateJSON()
      const JSON = this.JSONData
      this.$emit('TableData', {
        JSONData: JSON,
        tableLimit: this.onPageCount,
        rands: this.randWords
      })
    },
    resetData () {
      this.recordsCount = null
      this.onPageCount = null
      this.randWords = null
    },
    generateData () {
      const wordsArr = this.randWords.split(',')
      const arrayOfObjects = []
      for (let object = 1; object <= this.recordsCount; object++) {
        const createdObject = {
          id: object,
          title: `name ${object}`,
          rand: this.randomRand(wordsArr)
        }
        arrayOfObjects.push(createdObject)
      }
      this.preJSONdata = arrayOfObjects
    },
    randomRand (randArr) {
      const rand = randArr
      const randItem = rand[Math.floor(Math.random() * rand.length)]
      return randItem
    },
    generateJSON () {
      this.JSONData = JSON.stringify(this.preJSONdata)
      console.table(this.JSONData)
      console.log(this.JSONData)
    }
  }
}
</script>

<style></style>
