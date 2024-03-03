<template>
  <Header @setSearch="searchValue = $event" />
  <Notes :notes="filterNotes" @delNote="delNote" @change="change" />
  <Addbutton @openModal="openModal" />
  <Modal
    v-show="modalOpen"
    @closeModale="closeModale"
    @addNote="addNote"
    :edit="edit"
    :editNote="editNote"
    @changedNote="changedNote"
  />
</template>
<script>
import Header from "./components/Header.vue";
import Notes from "./components/Notes.vue";
import Addbutton from "./components/Addbutton.vue";
import Modal from "./components/Modal.vue";
export default {
  components: {
    Header,
    Notes,
    Addbutton,
    Modal,
  },
  data() {
    return {
      searchValue: "",
      modalOpen: false,
      notes: [],
      edit: false,
      editNote: null,
    };
  },

  computed: {
    filterNotes() {
      return this.searchValue
        ? this.notes.filter((note) =>
            note.title.toLowerCase().includes(this.searchValue.toLowerCase())
          )
        : this.notes;
    },
  },

  methods: {
    openModal() {
      this.modalOpen = true;
      this.edit = false;
    },
    closeModale(status) {
      this.modalOpen = status;
    },
    addNote(note) {
      //  console.log(note);
      this.notes.push(note);
      this.closeModale();
    },
    getNotes() {
      let locaNotes = localStorage.notes;
      if (locaNotes) {
        this.notes = JSON.parse(locaNotes);
      }
    },
    delNote(id) {
      // console.log(id);

      let index = this.notes.findIndex((item) => {
        return item.id == id;
      });

      this.notes.splice(index, 1);
    },
    change(id) {
      // console.log(id);
      this.modalOpen = this.edit = true;
      let currentNotem = this.notes.find((note) => note.id == id);
      this.editNote = currentNotem;
    },
    changedNote(newNote) {
      // console.log(newNote);
      this.notes.forEach((note) => {
        if (note.id == newNote.id) {
          note.title = newNote.title;
          note.text = newNote.text;
          note.date = newNote.date;
        }
      });
    },
  },
  watch: {
    notes: {
      handler() {
        localStorage.notes = JSON.stringify(this.notes);
      },
      deep: true,
    },
  },
  mounted() {
    this.getNotes();
  },
};
</script>

<style>
</style>