<template>
  <div class="note">
    <h4>{{note.name}}</h4>
    <img class="change-pencil" src="../../img/change-pencil.png" @click="$emit('changeNote', [note, index])"/>
    <img class="change-pencil" src="../../img/remove.png" @click="$emit('removeNote', index)"/>
    <ul>
      <li v-for="todo in note.todos" :key="todo.name" :class="{ 'done' : todo.done}">{{todo.name}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Note",
  props: {
    note: Object,
    index: Number,
  }
}
</script>