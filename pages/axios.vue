<template>
  <div>
    <article v-for="character in chars.results" :key="character.id">
      <h1>{{ character.name }}</h1>
    </article>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentPage: 1
    };
  },
  async asyncData({ $axios }) {
    try {
      const chars = await $axios.$get(
        "https://rickandmortyapi.com/api/character?page=1"
      );
      return { chars };
    } catch (error) {
      console.error(error);
    }
  }
};
</script>

<style></style>
