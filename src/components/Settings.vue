<template>
  <div class="settings">
    <label for="interval">interval</label>
    <input type="number" name="interval" v-model="interval">
    <label for="repeat">repeat</label>
    <input type="number" name="repeat" v-model="repeat">
    <label for="breakTime">breakTime</label>
    <input type="number" name="breakTime" v-model="breakTime">
    <label for="trackLength">trackLength</label>
    <input type="number" name="trackLength" v-model="trackLength">
  </div>
</template>

<script>
import { ref, watch, defineComponent } from 'vue';

export default defineComponent({

  name: 'Settings',

  setup(_, context) {
    const interval = ref(5)
    const repeat = ref(50)
    const breakTime = ref(10)
    const trackLength = ref(25)

    watch(interval, () => {
      context.emit('update-settings', interval.value, repeat.value, breakTime.value, trackLength.value)
    })

    watch(repeat, () => {
      context.emit('update-settings', interval.value, repeat.value, breakTime.value, trackLength.value)
    })

    watch(breakTime, () => {
      context.emit('update-settings', interval.value, repeat.value, breakTime.value, trackLength.value)
    })

    watch(trackLength, () => {
      context.emit('update-settings', interval.value, repeat.value, breakTime.value, trackLength.value)
    })

    return {
      interval,
      repeat,
      breakTime,
      trackLength
    }
  }
})
</script>

<style scoped>

</style>
