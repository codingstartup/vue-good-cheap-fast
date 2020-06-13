<template>
  <div id="app">
    <toggler :size="4" :checked="checked[0]" @updated="(value) => updatedHandler(0, value)">Good</toggler>
    <toggler :size="4" :checked="checked[1]" @updated="(value) => updatedHandler(1, value)">Cheap</toggler>
    <toggler :size="4" :checked="checked[2]" @updated="(value) => updatedHandler(2, value)">Fast</toggler>
  </div>
</template>

<script>
import Toggler from './components/Toggler.vue'

export default {
  name: 'App',
  components: {
    Toggler,
  },
  data() {
    return {
      checked: [false, false, false],
      indexes: [],
    }
  },
  methods: {
    updatedHandler(index, value) {
      if (value && !this.indexes.includes(index)) {
        let newIndexes = [...this.indexes]
        newIndexes.push(index)
        this.indexes = newIndexes
      }

      if (!value && this.indexes.includes(index)) {
        let newIndexes = [...this.indexes]
        newIndexes.splice(this.indexes.indexOf(index), 1)
        this.indexes = newIndexes
      }

      if (this.indexes.length === 3) {
        let newIndexes = [...this.indexes]
        newIndexes.splice(0, 1)
        this.indexes = newIndexes
      }

      let checked = [false, false, false]

      if (typeof this.indexes[0] !== 'undefined') {
        checked[this.indexes[0]] = true
      }

      if (typeof this.indexes[1] !== 'undefined') {
        checked[this.indexes[1]] = true
      }

      this.checked = checked
    }
  }
}
</script>

<style>
#app {
  font-family: Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  flex-direction: column;

}

body {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  margin: 0;
  padding: 0;
}
</style>
