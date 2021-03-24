<template>
  <div>
    <article v-for="character in characters" :key="character.id">
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
      const response = await $axios.$get(
        "http://localhost:8888/.netlify/functions/ram-axios"
      );
      console.log(response);
      return { characters: response.results };
    } catch (error) {
      console.error(error);
    }
  }
};
</script>

<style></style>
