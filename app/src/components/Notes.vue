<template>
  <div class="notes">
    <AddNote v-if="!changing" @addNote="onAddNote" />

    <ChangeNote v-if="changing" :changingNote="changingNote" @onChangingNote="onChangingNote" />

    <Note
      v-for="(note, index) in notes"
      v-else
      :key="index"
      :note="note"
      :index="index"
      @removeNote="onRemoveNote"
      @changeNote="onChangeNote"
    />

    <DialogWindow
      v-if="changeNote"
      :index="index"
      @confirmChange="onConfirmChange"
      @cancelChange="onCancelChange"
    />
  </div>
</template>

<script>
import AddNote from "./AddNote.vue";
import ChangeNote from "./ChangeNote.vue";
import Note from "./Note.vue";
import DialogWindow from "./DialogWindow.vue";
import NotesList from "../NotesList.js";

export default {
  name: 'Notes',

  components: {
    AddNote,
    ChangeNote,
    DialogWindow,
    Note,
  },

  data() {
    return {
      notes: JSON.parse(localStorage.getItem("notes")) || NotesList,
      changing: false,
      changingNote: {},
      changeNote: false,
      index: 0,
      addNotePage: false,
    }
  },

  methods: {

    onRemoveNote(index) {
      this.changeNote = true;
      this.index = index;
    },

    onChangeNote(arr) {
      this.changing = true;
      this.changingNote = arr[0];
      this.index = arr[1];
    },

    onChangingNote(note) {
      this.changing = false;
      this.notes[this.index] = note;
      localStorage.setItem("notes", JSON.stringify(this.notes));
    },

    onConfirmChange(index) {
      this.notes.splice(index, 1);
      this.index = 0;
      this.changeNote = false;
      localStorage.setItem("notes", JSON.stringify(this.notes));
    },

    onCancelChange() {
      this.changeNote = false;
    },

    onAddNote(note) {
      this.notes.push({ done: false, name: note[0], todos: [{ name: note[1], done: false }] });
      this.addNotePage = false;
      localStorage.setItem("notes", JSON.stringify(this.notes));
    }
  }
}
</script>