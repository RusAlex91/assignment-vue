<template>
  <div class="">
    <form action="" v-on:submit.prevent>
      <label>
        Entries to generate
        <input
          placeholder="0"
          v-model.number="recordsCount"
          type="number"
          class="records-number"
          requiered
        />
        <span
          :class="{ invisible: inputRecordError == '' }"
          class="text-danger inputError"
          >{{ this.inputRecordError }}</span
        >
      </label>
      <label>
        Entries on page limit
        <input
          placeholder="0"
          v-model.number="onPageCount"
          type="number"
          class="onpage-number"
          requiered
        />
        <span
          :class="{ invisible: inputPageError == '' }"
          class="text-danger inputError"
          >{{ this.inputPageError }}</span
        >
      </label>
      <label>
        Entries name to generate
        <input
          placeholder="apple, tomato"
          v-model="randWords"
          type="text"
          class="rand-words"
          requiered
        />
        <span
          :class="{ invisible: inputRandError == '' }"
          class="text-danger inputError"
          >{{ this.inputRandError }}</span
        >
      </label>
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
      JSONData: null,
      inputRecordError: '',
      inputPageError: '',
      inputRandError: ''
    }
  },
  methods: {
    applyData () {
      if (
        this.inputRecordError === '' &&
        this.inputPageError === '' &&
        this.inputRandError === ''
      ) {
        this.generateData()
        this.generateJSON()
        const JSON = this.JSONData
        this.$emit('TableData', {
          JSONData: JSON,
          tableLimit: this.onPageCount,
          rands: this.randWords
        })
      }
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
    }
  },
  watch: {
    randWords () {
      if (this.randWords === null) {
        this.inputRandError = ''
        return
      }
      const reg = /^\w+(?:(?:,\s\w+)+|(?:\s\w+)+)$/
      if (!reg.test(this.randWords)) {
        this.inputRandError =
          'Enter more than one word separated by commas and spaces'
      } else {
        this.inputRandError = ''
      }
    },
    recordsCount () {
      const reg = /[.]+/g
      if (this.recordsCount === null) {
        this.inputRecordError = ''
        return
      }
      if (this.recordsCount < 1 || reg.test(this.recordsCount)) {
        this.inputRecordError = 'Entries must be integer and more then zero'
      } else {
        this.inputRecordError = ''
      }
    },
    onPageCount () {
      const reg = /[,]+/g
      if (this.onPageCount === null) {
        this.inputPageError = ''
        return
      }
      if (this.onPageCount < 1 || reg.test(this.recordsCount)) {
        this.inputPageError =
          'Entries max rows must be more then zero and integer'
      } else {
        this.inputPageError = ''
      }
    }
  }
}
</script>

<style>
.invisible {
  visibility: hidden;
}

.inputError {
  position: absolute;
  top: 10;
}

form input {
  display: flex;
  margin-right: 10px;
}

form label {
  margin-bottom: 60px;
  position: relative;
}

form button {
  margin-right: 10px;
}
</style>
