<template>
  <div class='main'>
    <h1>Pass Mob Baton</h1>
    <members @join-session="joinSession"/>
    <attendees @leave-session="leaveSession" :attendees="state.attendees"/>
  </div>
</template>

<script>
import Members from './components/Members.vue';
import Attendees from './components/Attendees.vue';

import { defineComponent, reactive } from "vue";

export default defineComponent({
  components: {
    Members,
    Attendees,
  },
  setup() {
    const state = reactive({
      attendees: [],
    })

    const joinSession = (attendee) => {
      state.attendees.push(attendee)
    }

    const leaveSession = (attendee) => {
      state.attendees.splice(attendee, 1)
    }

    return {
      state,
      joinSession,
      leaveSession,
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
