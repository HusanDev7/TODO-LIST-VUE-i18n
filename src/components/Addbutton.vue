<template>
  <button class="addBtn" @click="$emit('openModal')">
    <img src="@/assets/img/pencil.svg" alt="" />
  </button>
</template>

<script>
export default {};
</script>

<style>
.addBtn {
  background: var(
    --m-3-read-only-light-surface-3,
    linear-gradient(
      0deg,
      rgba(103, 80, 164, 0.11) 0%,
      rgba(103, 80, 164, 0.11) 100%
    ),
    #fffbfe
  );
  box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15),
    0px 1px 2px 0px rgba(0, 0, 0, 0.3);
  border-radius: 16px;
  border: none;
  width: 56px;
  height: 56px;
  cursor: pointer;
  position: fixed;
  right: 30px;
  bottom: 30px;
}
</style>