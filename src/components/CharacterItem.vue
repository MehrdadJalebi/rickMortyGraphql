<script setup>
defineProps({
  character: {
    type: Object,
    required: true,
  },
});
</script>

<template>
  <div class="item">
    <h3>{{ character.name }}</h3>
  </div>
</template>

<style scoped>
.item {
  margin: 1rem auto;
  display: flex;
  border: 1px solid var(--color-text);
  border-radius: 1rem;
  padding: 1.5rem;
  width: 70vw;
}


i {
  display: flex;
  place-items: center;
  place-content: center;
  width: 32px;
  height: 32px;
  color: var(--color-text);
}

h3 {
  font-size: 1.2rem;
  font-weight: 500;
  color: var(--color-heading);
}
</style>
