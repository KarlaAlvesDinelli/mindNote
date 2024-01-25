<template>
  <div class="ui visible inverted left vertical sidebar menu">
    <!-- Logo -->
    <div class="item logo"><i class="icon star"></i> Mind Note</div>
    <!-- Linha de separação -->
    <div class="ui horizontal divider"></div>
    <!-- Título "Minhas Notas" -->
    <div
      class="item header"
      style="font-size: 1.2em; display: flex; align-items: center"
    >
      Minhas Notas
    </div>
    <!-- Notas -->
    <div
      class="item"
      v-for="note in notes"
      :key="note.title"
      @click="selectNote(note)"
    >
      {{ note.title }}
      <i class="trash icon" @click.stop="deleteNoteSidebar(note)"></i>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    notes: Array,
  },
  methods: {
    selectNote(note) {
      this.$emit("selectNote", note);
    },
    deleteNoteSidebar(note) {
      const ifRemove = confirm(
        "Você tem certeza que deseja deletar esta nota?"
      );
      if (ifRemove) {
        this.$emit("deleteNoteSidebar", note);
        alert("Note deleted");
      }
    },
  },
};
</script>

<style scoped>
/* Adicione estilos específicos da barra lateral aqui se necessário */
.logo {
  font-size: 1.5em;
  font-weight: bold;
  margin: 1em 0;
}
</style>
