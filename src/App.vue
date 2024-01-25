<template>
  <div>
    <SidebarApp
      :notes="notes"
      @selectNote="selectNote"
      @deleteNoteSidebar="deleteNoteSidebar"
      @editNoteSidebar="editNoteSidebar"
    />
    <CreateNote v-on:SeDataToCnote="CreateNote" />
    <!-- Modal de Edição (App) -->
    <div class="ui modal" :class="{ active: isEditModalActive }">
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
    <ViewNote :selectedNote="selectedNote" @editNote="openEditModalApp" />
  </div>
</template>

<script>
import CreateNote from "./components/create-notes.vue";
import SidebarApp from "./components/SidebarApp.vue";
import ViewNote from "./components/ViewNote.vue";

export default {
  name: "App",
  components: {
    CreateNote,
    SidebarApp,
    ViewNote,
  },
  data() {
    return {
      notes: [
        {
          title: "Minha primeira nota!",
          description: "Minha primeira nota!",
        },
        {
          title: "Minha segunda nota!",
          description: "Minha segunda nota!",
        },
        {
          title: "Minha Terceira nota!",
          description: "Minha Terceira nota!",
        },
      ],
      selectedNote: null,
      isEditModalActive: false,
      editedTitle: "",
      editedDescription: "",
    };
  },
  methods: {
    CreateNote(note) {
      this.notes.push(note);
      alert("Nota Adicionada com Sucesso!");
    },
    deleteNoteSidebar(note) {
      const index = this.notes.indexOf(note);
      if (index !== -1) {
        this.notes.splice(index, 1);
      }
    },
    editNoteSidebar(editedNote) {
      const originalNote = this.notes.find((n) => n === this.selectedNote);
      if (originalNote) {
        originalNote.title = editedNote.title;
        originalNote.description = editedNote.description;
        this.isEditModalActive = false;
        this.selectedNote = null;
      }
    },
    selectNote(note) {
      this.selectedNote = note;
    },
    openEditModalApp() {
      this.openEditModal();
    },
    openEditModal() {
      this.isEditModalActive = true;
      this.editedTitle = this.selectedNote.title;
      this.editedDescription = this.selectedNote.description;
    },
    closeEditModal() {
      this.isEditModalActive = false;
    },
    saveEdits() {
      this.editNoteSidebar({
        title: this.editedTitle,
        description: this.editedDescription,
      });
      this.isEditModalActive = false;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.ui.modal {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  max-width: 80%;
  max-height: 80vh;
}
</style>
