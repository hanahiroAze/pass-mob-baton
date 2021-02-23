<template>
  <div class='main'>
    <h1>Pass Mob Baton</h1>
    <settings @update-settings="updateSettings"/>
    <members @join-session="joinSession"/>
    <attendees @leave-session="leaveSession" :attendees="state.attendees"/>
    <timer :interval="state.interval" :repeat="state.repeat" :breakTime="state.breakTime" :trackLength="state.trackLength" />
  </div>
</template>

<script>
import Members from './components/Members.vue';
import Attendees from './components/Attendees.vue';
import Settings from './components/Settings.vue';
import Timer from './components/Timer.vue';

import { defineComponent, reactive } from "vue";

export default defineComponent({
  components: {
    Members,
    Attendees,
    Settings,
    Timer,
  },
  setup() {
    const state = reactive({
      attendees: [],
      interval: 5,
      repeat: 5,
      breakTime: 10,
      trackLength: 25
    })

    const joinSession = (attendee) => {
      state.attendees.push(attendee)
    }

    const leaveSession = (attendee) => {
      state.attendees.splice(attendee, 1)
    }

    const updateSettings = (interval, repeat, breakTime, trackLength) => {
      state.interval = parseInt(interval)
      state.repeat = parseInt(repeat)
      state.breakTime = parseInt(breakTime)
      state.trackLength = parseInt(trackLength)
    }

    return {
      state,
      joinSession,
      leaveSession,
      updateSettings
    }
  }
})
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
