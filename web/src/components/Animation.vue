<template>
  <div>
    <transition name="slide-fade">
      <div v-if="show">
        <p>Home page</p>
        <p>Random number from backend: {{ randomNumber }}</p>
      <button @click="getRandom">New random number</button>
      </div>
    </transition>

    <div id="example-1">
      <button @click="show = !show">
        Toggle render
      </button>
      <transition name="slide-fade">
        <p v-if="show">hello</p>
      </transition>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      show: true,
      randomNumber: 0
    }
  },
  methods: {
    getRandomInt (min, max) {
      min = Math.ceil(min)
      max = Math.floor(max)
      return Math.floor(Math.random() * (max - min + 1)) + min
    },
    getRandom () {
      // this.randomNumber = this.getRandomInt(1, 100)
      this.randomNumber = this.getRandomFromBackend()
    },
    getRandomFromBackend () {
      const path = `http://localhost:5000/api/random`;
      axios.get(path).then(response => {
          this.randomNumber = response.data.randomNumber
      }).catch(error => {
          console.log(error)
      })
    }
  },
  created () {
    this.getRandom()
  }
}
</script>


<style scoped>
.slide-fade-enter-active {
  transition: all .3s ease;
}
.slide-fade-leave-active {
  transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active below version 2.1.8 */ {
  transform: translateX(10px);
  opacity: 0;
}
</style>
