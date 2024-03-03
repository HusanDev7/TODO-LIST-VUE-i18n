<template>
  <div class="note">
    <div class="container">
      <div class="note__top">
        <h2 class="note__top-title">
          {{ notes.length > 0 ? $t("allNotes") : $t("noNotes") }}
        </h2>
        <button class="note__top-btn" @click="show">
          <img src="@/assets/img/grid.svg" alt="" v-if="toggle" />
          <img src="@/assets/img/flex.svg" alt="" v-else />
          <span class="note__top-span">
            {{ toggle ? "Roʻyxat" : "Setka" }}
          </span>
        </button>
      </div>

      <div class="note__list" :class="{ flex: !toggle }">
        <NoteItem
          v-for="note in notes"
          :key="note.id"
          :note="note"
          @change="$emit('change', note.id)"
          @dellNote="$emit('delNote', note.id)"
        />
      </div>
    </div>
  </div>
</template>

<script>
import NoteItem from "./NoteItem.vue";

export default {
  components: {
    NoteItem,
  },
  props: {
    notes: {
      typeof: Array,
    },
  },

  data() {
    return {
      toggle: true,
    };
  },
  methods: {
    show() {
      this.toggle = !this.toggle;
    },
  },
};
</script>

<style>
</style>