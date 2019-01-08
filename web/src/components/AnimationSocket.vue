<template>
  <div>
    <h1>eugenechung81 has purchased $25 Sneak product</h1>
    <form method="post" action="#" id="cityform">
        <label>City</label>
        <input type="text" id="city"></input>
        <input type="submit" value="Submit"></input>
    </form>
    <transition name="slide-fade">
      <div v-if="show" id="cities-list"></div>
    </transition>
</div>
</template>

<script>

$(document).ready(function () {
  var url = "http://" + document.domain + ":" + '5000';
  var socket = io.connect(url + "/dd");

  $("#cityform").submit(function (event) {
    socket.emit('city', {'city': $('#city').val()});
    $('#city').val('');
    return false;
  });

  socket.on('city', function (msg) {
    $("#cities-list").prepend('<h3>' + msg.city + '<h3>');
  });

});

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
