<template>
  <div class="note__list-item">
    <div class="note__list-item-top">
      <h3 class="note__title">{{ note.title }}</h3>
      <p class="note__date">{{ note.date }}</p>
    </div>
    <p class="note__list-item-desc">
      {{ note.text }}
    </p>
    <div class="note__list-item-btns">
      <button @click="$emit('change', note.id)">
        <img src="@/assets/img/pencil.svg" alt="" />
        <span class="note__edit">O'ZGARTIRISH</span>
      </button>
      <button @click="$emit('dellNote', note.id)">
        <img src="@/assets/img/cart.svg" alt="" />
        <span class="note__dell">o'chirish</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    note: {
      typeof: Object,
    },
  },
};
</script>

<style>
</style>