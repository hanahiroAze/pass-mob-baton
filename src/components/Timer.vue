<template>
  <div class="timer">
    <h2>{{ timeLeft }}</h2>
    <button @click="startStop" v-if="!timerOn">Start</button>
    <button @click="startStop" v-if="timerOn">Stop</button>
  </div>
</template>

<script>
import { ref, reactive, computed, defineComponent, watch } from 'vue';

export default defineComponent({
  props: {
    interval: {
      type: Number,
      default: 0
    },
    repeat: {
      type: Number,
      default: 0
    },
    breakTime: {
      type: Number,
      default: 0
    },
    trackLength: {
      type: Number,
      default: 0
    }
  },

  name: 'Timer',

  setup(props) {
    const min = ref(props.interval)
    const sec = ref(0)
    const timerOn = ref(false)
    const timer = ref(null)

    const timeLeft = computed(() => {
      return presentTime()
    })

    function presentTime() {
      let timeStrings = [
        min.value.toString(),
        sec.value.toString()
      ].map(function(str) {
        if (str.length < 2) {
          return "0" + str
        } else {
          return str
        }
      })
      return timeStrings[0] + ":" + timeStrings[1]
    }

    function startStop() {
      timerOn.value = !timerOn.value
      
      if (timerOn.value) {
        timer.value = setInterval(function() {count()}, 1000)
      } else {
        complete(timer.value)
      }
    }

    function count() {
      if (sec.value <= 0 && min.value >= 1) {
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
      min,
      sec,
      timerOn,
      timer,
      timeLeft,
      startStop,
    }
  }
})
</script>

<style scoped>

</style>
