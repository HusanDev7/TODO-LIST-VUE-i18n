<template>
  <header class="header">
    <nav class="nav shadow" v-if="header">
      <button class="nav__lang" @click="switchLange">{{ $i18n.locale }}</button>
      <h3 class="nav__title">{{ $t("notes") }}</h3>
      <button class="nav__search" @click="headerShow">
        <img src="@/assets/img/search.svg" alt="" />
      </button>
    </nav>

    <nav class="nav__search shadow" v-else>
      <div class="nav__search-opt">
        <button class="nav__search-opt-btn" @click="headerShow">
          <img src="@/assets/img/arrow.svg" alt="" />
        </button>
        <input
          v-model="search"
          placeholder="Qidirish..."
          type="text"
          class="nav__search-inp"
        />
      </div>
      <button class="nav__search-btn" @click="inputClear">
        <img src="@/assets/img/close.svg" alt="" />
      </button>
    </nav>
  </header>
</template>
<script>
export default {
  data() {
    return {
      header: true,
      search: "",
    };
  },
  methods: {
    headerShow() {
      this.header = !this.header;
    },
    inputClear() {
      this.search = "";
    },
    switchLange() {
      this.$i18n.locale == "ru"
        ? (this.$i18n.locale = "uz")
        : (this.$i18n.locale = "ru");
      localStorage.lang = this.$i18n.locale;
    },
  },
  watch: {
    search(newVal) {
      // console.log(newVal);
      this.$emit("setSearch", newVal);
    },
  },
};
</script>

<style>
</style>