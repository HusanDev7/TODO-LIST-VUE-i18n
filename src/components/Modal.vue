<template>
  <Transition name="modal">
    <div class="modal" @click="closeModale">
      <div class="modal__block" @click.stop="">
        <h3 class="modal__title">
          {{ edit ? "Eslatma O'zgartirish" : "Eslatma qo’shish" }}
        </h3>
        <div class="modal__inputs">
          <label>
            <span>Title</span>
            <input v-model="title" type="text" placeholder="Title" />
          </label>
          <label>
            <span>Content</span>
            <input v-model="text" type="text" placeholder="Content" />
          </label>
        </div>
        <div class="modal__btns">
          <button class="btn red" @click="closeModale">Bekor qilish</button>
          <button class="btn puple" @click="addNote" v-if="!edit">
            Qo’shish
          </button>
          <button class="btn puple" v-else @click="changeNote">
            o'zgartirish
          </button>
        </div>
      </div>
    </div>
  </Transition>
</template>

<script>
let id = 0;
export default {
  props: {
    edit: {
      typeof: Boolean,
    },
    editNote: {
      typeof: Object,
    },
  },

  data() {
    return {
      title: "",
      text: "",
    };
  },
  methods: {
    addNote() {
      if (this.title != "" && this.text != "") {
        const notes = {
          id: id++,
          title: this.title,
          text: this.text,
          date: new Date().toLocaleDateString(),
        };
        this.title = "";
        this.text = "";

        this.$emit("addNote", notes);
       
      }
    },
    closeModale() {
      this.$emit("closeModale", false);
    },
    changeNote() {
      const newEditedNote = {
        id: this.editNote.id,
        title: this.title,
        text: this.text,
        date: new Date().toLocaleDateString(),
      };
      this.$emit("changedNote", newEditedNote);
      this.closeModale()
    },
  },
};
</script>

<style>
.modal-enter-active,
.modal-leave-active {
  transition: opacity 0.5s ease;
}

.modal-enter-from,
.modal-leave-to {
  opacity: 0;
}
</style>