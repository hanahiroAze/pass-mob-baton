<template>
  <div class="timer">
    <h2>{{ timeLeft }}</h2>
    <button @click="startStop" v-if="!timerOn">Start</button>
    <button @click="startStop" v-if="timerOn">Stop</button>
  </div>
</template>

<script>
import { ref, computed, defineComponent } from 'vue';

export default defineComponent({
  props: {
    interval: {
      type: Number,
      default: 5
    }
  },

  name: 'Timer',

  setup() {
    const hour = ref(10)
    const min = ref(59)
    const sec = ref(59)
    const timerOn = ref(false)
    const timer = ref(null)

    const timeLeft = computed(() => {
      let timeStrings = [
        hour.value.toString(),
        min.value.toString(),
        sec.value.toString()
      ].map(function(str) {
        if (str.length < 2) {
          return "0" + str
        } else {
          return str
        }
      })
      return timeStrings[0] + ":" + timeStrings[1] + ":" + timeStrings[2]
    })

    function startStop() {
      timerOn.value = !timerOn.value
      
      if (timerOn.value) {
        timer.value = setInterval(function() {count()}, 1000)
      } else {
        complete(timer.value)
      }
    }

    function count() {
      if (hour.value <= 0 && min.value >= 1) {
        hour.value --
        min.value = 59
      } else if (sec.value <= 0 && min.value >= 1) {
        min.value --
        sec.value = 59
      } else if(sec.value <= 0 && min.value <= 0) {
        complete(timer.value)
      } else {
        sec.value --;
      }
    }

    function complete(timer) {
      clearInterval(timer)
    }

    return {
      hour,
      min,
      sec,
      timerOn,
      timer,
      timeLeft,
      startStop,
      count,
      complete,
    }
  }
})
</script>

<style scoped>

</style>
