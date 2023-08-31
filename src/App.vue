<template>
  <main>
    <MonetoryButton :btnText="'Нажми меня!'" :btnColor="`purple`" />
  </main>
</template>

<script setup lang="ts">
import MonetoryButton from "./components/MonetoryButton.vue";
</script>
<style>
* {
  box-sizing: border-box;
}
</style>
