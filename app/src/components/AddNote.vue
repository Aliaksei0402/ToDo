<template>
  <div class="add-note">
      <span>Имя заметки</span>
      <input type="text" v-model="nameNote"/>
      <span>todo</span>
      <input type="text" v-model="todo"/>
      <button class="add-button" @click="$emit('addNote', [nameNote, todo])">Add new note</button>
  </div>
</template>

<script>
export default {
    name: "AddNote",
    data() {
        return {
            nameNote: "",
            todo: [],
        }
    }
}
</script>