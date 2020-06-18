<template>
  <div class="add-note">
    <input type="text" v-model="nameNote" placeholder="Note name" />
    <input type="text" v-model="todo" placeholder="Todo" />
    <img class="add-note-button" src="../../img/add.png" @click="emptyInputs(), cleanInputs()" />
  </div>
</template>

<script>
export default {
  name: 'AddNote',

  data() {
    return {
      nameNote: "",
      todo: "",
    }
  },

  methods: {
    cleanInputs() {
      this.nameNote = "";
      this.todo = "";
    },

    emptyInputs() {
      if (this.nameNote === "" || this.todo === "") {
        return;
      }
      this.$emit('addNote', [this.nameNote, this.todo])
    }
  }
}
</script>