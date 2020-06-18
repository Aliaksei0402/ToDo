<template>
  <div class="change-note">
    <h2>Edit Note</h2>
    <div class="edit">
      <div class="edit-buttons">
        <button @click="cancelChange">Discard Changes</button>
        <button @click="cancelCancelChange" :disabled="disabled">Return Change</button>
        <button @click="cancelEditingWindow">Exit</button>
      </div>

      <DialogWindow
        v-if="canselEdition"
        @confirmChange="onConfirmChange"
        @cancelChange="onCancelChange"
      />

      <input type="text" v-model="note.name" />
      <ul>
        <li v-for="(todo, index) in note.todos" :key="index">
          <input type="checkbox" v-model="todo.done" @click="todo.done = !todo.done" />
          <input type="text" v-model="todo.name" />
          <img class="remove-todo" src="../../img/remove.png" @click="removeTodo(index)" />
        </li>
        <li>
          <input
            type="checkbox"
            v-model="checkboxAddedTodo"
            @click="checkboxAddedTodo = !checkboxAddedTodo"
          />
          <input type="text" v-model="addedTodo" placeholder="Enter New Todo" />
          <img class="remove-todo" src="../../img/add.png" @click="onAddTodo" />
        </li>
      </ul>

      <div class="add-new-todo"></div>
      <button class="save-changes" @click="$emit('onChangingNote', note)">Save changes</button>
    </div>
  </div>
</template>

<script>
import DialogWindow from "./DialogWindow.vue";

export default {
  name: 'ChangeNote',

  components: {
    DialogWindow,
  },

  props: {
    changingNote: Object,
  },

  data() {
    return {
      note: JSON.parse(JSON.stringify(this.changingNote)),
      addedTodo: '',
      checkboxAddedTodo: false,
      canselEdition: false,
      cancelCanseledNote: {},
      disabled: true,
    }
  },

  methods: {
    onAddTodo() {
      if (this.addedTodo === "") {
        return;
      }
      this.note.todos.push({ done: this.checkboxAddedTodo, name: this.addedTodo });
      this.addedTodo = '';
      this.checkboxAddedTodo = false;
    },

    cancelChange() {
      this.cancelCanseledNote = this.note;
      this.note = JSON.parse(JSON.stringify(this.changingNote));
      this.disabled = false;
    },

    cancelCancelChange() {
      this.note = this.cancelCanseledNote;
      this.disabled = true;
    },

    removeTodo(index) {
      this.note.todos.splice(index, 1);
    },

    cancelEditingWindow() {
      this.canselEdition = true;
    },

    onConfirmChange() {
      this.$emit('onChangingNote', this.note);
      this.canselEdition = false;
    },

    onCancelChange() {
      this.canselEdition = false;
    }
  }
}
</script>