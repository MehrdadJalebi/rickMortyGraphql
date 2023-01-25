<script setup>
import CharacterItem from "./CharacterItem.vue";
import gql from 'graphql-tag'
import { useQuery } from '@vue/apollo-composable'

const CHARACTERS_QUERY = gql`
  query Characters {
    characters {
      results {
        id
        name
        image
      }
    }
  }
`

const { result, loading, error } = useQuery(CHARACTERS_QUERY);
</script>

<template>
  <div class="list">
    <p v-if="error">Something went wrong...</p>
    <img src="@/assets/loading.svg" v-if="loading" />
    <p v-else v-for="character in result.characters.results" :key="character.id">
    <CharacterItem :character="character" />
    </p>
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
