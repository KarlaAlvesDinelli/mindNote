<template>
  <tnotes
    v-on:DeleteN="deleteNoteSE"
    v-for="note in notesd"
    :key="note"
    :notesL="note"
  />
</template>
<script>
import Tnotes from "./TextNote.vue";
export default {
  props: ["notesd"],
  components: {
    Tnotes,
  },
  methods: {
    deleteNoteSE(note) {
      var ifRemove = confirm("Você tem certeza que deseja deletar esta nota?");
      if (ifRemove) {
        const ThisNote = this.notesd;
        const indexOFNote = ThisNote.indexOf(note);
        ThisNote.splice(indexOFNote, 1);
        alert("Nota deletada com sucesso!");
      }
    },
  },
};
</script>
