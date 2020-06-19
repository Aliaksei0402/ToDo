<template>
  <div class="note">
    <div class="images">
      <img
        class="change-pencil"
        src="../../img/change-pencil.png"
        @click="$emit('changeNote', [note, index])"
      />
      <span class="note-name">{{note.name}}</span>
      <img class="delete" src="../../img/remove.png" @click="$emit('removeNote', index)" />
    </div>
    
    <ul>
      <li v-for="todo in note.todos" :key="todo.name" :class="{ 'done' : todo.done}" class="todo-li">{{todo.name}}</li>
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