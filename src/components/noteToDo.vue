<template>
  <div class="notes">
    <div>
      <input
        type="text"
        placeholder="введите текст..."
        v-model="textNote"
        @keydown.enter="addNote"
      />
      <button @click="addNote">add</button>
    </div>
    <ul class="note" v-for="(note, idx) in innerNotes" :key="idx">
      <div @click="editNote(idx)">{{ note }}</div>
      <button @click="delNote(idx)">-</button>
    </ul>
  </div>
</template>
<script lang="ts">
import { Vue, Options } from "vue-class-component";
@Options<NoteToDo>({
  props: {
    notes: [],
  },

  watch: {
    notes(value) {
      this.innerNotes = this.notes;
    },
  },
  emits: ["update:notes"],
})
export default class NoteToDo extends Vue {
  readonly notes = [];
  innerNotes = ["TEST1", "test2"];
  textNote = "";
  mounted() {
    this.innerNotes = this.notes;
  }
  delNote(id: number) {
    this.innerNotes.splice(id, 1);
  }
  addNote() {
    if (this.editIdx == -1) {
      this.innerNotes.push(this.textNote);
    } else {
      this.innerNotes[this.editIdx] = this.textNote;
      this.editIdx = -1;
    }
    this.$emit("update:notes", this.innerNotes);
    this.textNote = "";
  }
  editIdx = -1;
  editNote(idx: number) {
    this.editIdx = idx;
    this.textNote = this.innerNotes[idx];
  }
}
</script>
<style lang="less">
.notes {
  background: olive;
  padding: 10px;
  margin: 5px;
  .note {
    display: flex;
    justify-content: space-between;
    cursor: pointer;
    &:hover {
      text-decoration: underline;
    }
  }
}
</style>
