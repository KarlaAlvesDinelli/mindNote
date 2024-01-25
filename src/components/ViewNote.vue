<template>
  <div v-if="selectedNote">
    <h2>{{ selectedNote.title }}</h2>
    <p>{{ selectedNote.description }}</p>
    <button class="ui button" @click="openEditModal">Editar Nota</button>

    <!-- Modal de Edição -->
    <div class="ui modal centered" :class="{ active: isEditModalActive }">
      <div class="header">Editar Nota</div>
      <div class="content">
        <div class="ui form">
          <div class="field">
            <label>Título</label>
            <input type="text" v-model="editedTitle" />
          </div>
          <div class="field">
            <label>Descrição</label>
            <input type="text" v-model="editedDescription" />
          </div>
        </div>
      </div>
      <div class="actions">
        <div class="ui button" @click="closeEditModal">Cancelar</div>
        <div class="ui primary button" @click="saveEdits">Salvar</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["selectedNote"],
  data() {
    return {
      isEditModalActive: false,
      editedTitle: "",
      editedDescription: "",
    };
  },
  methods: {
    openEditModal() {
      this.isEditModalActive = true;
      // Preencha os campos de edição com os dados atuais da nota
      this.editedTitle = this.selectedNote.title;
      this.editedDescription = this.selectedNote.description;
    },
    closeEditModal() {
      this.isEditModalActive = false;
    },
    saveEdits() {
      // Emitir evento para o componente pai com os dados editados
      this.$emit("editNote", {
        title: this.editedTitle,
        description: this.editedDescription,
      });
      this.isEditModalActive = false;
    },
  },
};
</script>

<style scoped>
/* Adicione estilos específicos para centralizar o modal */
.ui.modal.centered {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  max-width: 80%; /* Ajuste o valor conforme necessário */
  max-height: 80vh; /* Ajuste o valor conforme necessário */
}
</style>
