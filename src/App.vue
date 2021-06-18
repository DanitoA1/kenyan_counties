<template>
  <div id="app">
    <h1>A simple Application to Convert Kenyan Counties and Sub Counties Json Structure into the Required Json Structure</h1>
    <button @click="convertFormat()">Convert Now</button>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import kenyanCounties from '@/kenyan_counties.json'

export default {
  name: 'App',
  components: {
    // HelloWorld
  },
  data() {
    return {
      originalJson: [],
      newJson: []
    }
  },
  methods: {
    convertFormat () {
      this.originalJson = JSON.parse(JSON.stringify(kenyanCounties))
      this.originalJson.forEach((x, i) => {
        this.newJson.push(
          {
            state: {
              name: x.name,
              id: x.code,
              locals: []
            }
          },
        )
        x.sub_counties.forEach((y, ii) => {
          this.newJson[i].state.locals.push(
            {
              name: y,
              id: ii + 1
            }
          )
        })
      })
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
