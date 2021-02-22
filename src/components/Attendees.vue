<template>
  <div class="attendees">
    <label for="attendees">
      Attendees
    </label>
    <ul>
      <li v-for="attendee in attendees">
        {{attendee.name}}
        <button @click="leaveSession(attendee.name)">Leave</button>
        </li>
    </ul>
    <button @click="resetAllAttendees()">Reset Session</button>
  </div>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  props: {
    attendees: {
      type: Array,
      default: []
    }
  },

  name: 'Attendees',

  setup(props, context) {
    
    function leaveSession(name) {
      context.emit('leave-session', name)
    }
    
    return {
      leaveSession,
    }
  }
})
</script>

<style scoped>

</style>
