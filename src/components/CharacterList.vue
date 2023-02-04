<script setup>
import {computed} from "vue";
import CharacterItem from "./CharacterItem.vue";
import gql from 'graphql-tag'
import { useQuery } from '@vue/apollo-composable'

const CHARACTERS_QUERY = gql`
  query Characters ($page: Int) {
    characters (
      page: $page
    ) {
      results {
        id
        name
        image
      }
    }
  }
`
const { result, loading, error, fetchMore } = useQuery(CHARACTERS_QUERY, { variables: { page: 1 }});
const characters = computed(() => {
  return result.value?.characters.results
});
const scrollEnd = () => fetchMore({
  variables: {
    page: characters.length / 20 + 1
  },
  updateQuery: (prev, { fetchMoreResult }) => {
    if (!fetchMoreResult) return prev;
    return {
      characters: {
        __typename: 'Characters',
        results: [
          ...prev.characters.results,
          ...fetchMoreResult.characters.results
        ]
      }
    }
  }
})
</script>

<template>
  <div class="list">
    <p v-if="error">Something went wrong...</p>
    <img src="@/assets/loading.svg" v-if="loading" />
    <p v-else v-for="character in characters" :key="character.id">
    <CharacterItem :character="character" />
    </p>
    <button
      @click="scrollEnd"
    >
      Load More
    </button>
  </div>
</template>
<style scoped>
.list {
  margin: 3rem 6rem;
  display: flex;
  padding: 1rem;
  align-items: center;
  flex-flow: column;
  height: 80vh;
}
</style>
