<template>
  <div class="members">
    <form @submit.prevent="addNewMember">
      <label>New Member</label>
      <input type="text" name="newMember" v-model="newMember">
      <button>Add New Member</button>
    </form>
    <label for="team">
      Team Members
    </label>
    <ul>
      <li v-for="member in members">
        {{member.name}}
        <button @click="attend(member)">Attend</button>
        <button @click="removeMember(member.name)">Remove</button>
      </li>
    </ul>
    <button @click="resetAllMembers()">Reset Memvers</button>
  </div>
</template>

<script>
import { ref, defineComponent } from 'vue';

export default defineComponent({
  name: 'Members',

  setup(_, context) {
    const newMember = ref('');
    const members = ref([]);

    function addNewMember() {
      members.value.push({
        name: newMember.value,
      })
      newMember.value = ''
    }

    function removeMember(name) {
      members.value.splice(name, 1)
    }

    function resetAllMembers() {
      members.value = []
    }

    function attend(member) {
      context.emit("join-session", member)
    }

    return {
      addNewMember,
      removeMember,
      resetAllMembers,
      attend,
      newMember,
      members,
    };
  }
})
</script>

<style scoped>

</style>
