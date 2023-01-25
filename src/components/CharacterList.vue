<script setup>
//import CharacterItem from "./CharacterItem.vue";
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
  <!--<CharacterItem />-->
  <p v-if="error">Something went wrong...</p>
  <p v-if="loading">Loading...</p>
  <p v-else v-for="character in result.characters.results" :key="character.id">
    {{ character.name }}
  </p>
  <div></div>
</template>
