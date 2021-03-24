<template>
  <div>
    <article v-for="character in characters" :key="character.id">
      {{ character.name }}
    </article>
  </div>
</template>

<script>
import gql from "graphql-tag";
const GET_CHARACTERS = gql`
  query {
    characters(page: 2, filter: { name: "rick" }) {
      info {
        count
      }
      results {
        name
      }
    }
    location(id: 1) {
      id
    }
    episodesByIds(ids: [1, 2]) {
      id
    }
  }
`;
export default {
  async asyncData(context) {
    let client = context.app.apolloProvider.defaultClient;
    const { data } = await client.query({ query: GET_CHARACTERS });
    console.log(data);
    return { characters: data.characters.results };
  }
};
</script>

<style></style>
